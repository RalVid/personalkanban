# Tombstone Pattern Implementation for Deletion Sync

## Problem
When items were deleted from the kanban board, they were completely removed from the database. This made it impossible to sync deletions between devices - if an item was deleted on Device A, Device B had no way of knowing it should also remove that item during sync.

## Solution: Tombstone Pattern
Instead of permanently deleting items, we now mark them as deleted with a timestamp. This allows deletions to be properly synced across all devices.

## Changes Made

### 1. Modified `removeTask()` function
- Instead of `splice()` to remove items, tasks are now marked with:
  - `deleted: true`
  - `deletedAt: Date.now()`
- This preserves the task in the database but marks it as deleted

### 2. Updated `render()` function
- Added filter: `.filter(task => !task.deleted)`
- Only non-deleted tasks are displayed in the UI
- Deleted tasks remain in the data structure for sync purposes

### 3. Updated `undo` functionality
- When undoing a deletion, we now remove the `deleted` and `deletedAt` flags
- Previously restored by pushing back to array

### 4. Added `cleanupOldDeletedTasks()` function
- Automatically removes tasks that have been deleted for more than 30 days
- Runs on app load (after 3 seconds)
- Runs daily via `setInterval()`
- Prevents the database from growing indefinitely with old deleted items

### 5. Enhanced merge logic (2 locations)
- Updated both merge scenarios to use `Map` structures for better tracking
- Properly handles deleted tasks during cloud/local sync
- Respects deletions from both sources
- Adds new offline tasks while maintaining deleted state

### 6. Updated `hasLocalData` checks (2 locations)
- Now filters out deleted tasks when checking if local data exists
- Prevents false positives from data containing only deleted tasks

## How It Works

### Deletion Flow
1. User deletes a task
2. Task is marked `deleted: true` with `deletedAt: timestamp`
3. Task is hidden from UI but remains in database
4. Change syncs to cloud with tombstone intact
5. Other devices receive the update and also hide the task

### Sync Scenarios

#### Scenario 1: Task deleted on Device A, Device B syncs
- Device A: Task marked as deleted
- Sync occurs
- Device B: Receives task with `deleted: true`, filters it from view

#### Scenario 2: Task deleted offline, then comes back online
- Offline: Task marked as deleted locally
- Come online: Local deleted task syncs to cloud
- Cloud now has deleted task
- All other devices receive the deletion on next sync

#### Scenario 3: Cleanup after 30 days
- Task has `deletedAt` older than 30 days
- `cleanupOldDeletedTasks()` permanently removes it
- Prevents database bloat
- 30 days is sufficient for most sync scenarios

## Benefits

1. **Reliable Deletion Sync**: Deletions now properly propagate across all devices
2. **Undo Support**: Undo still works within the 5-second window
3. **Automatic Cleanup**: Old deletions are cleaned up automatically
4. **Backward Compatible**: Existing tasks without `deleted` flag work normally
5. **No Data Loss**: Deleted items are preserved for 30 days

## Technical Details

### Storage Impact
- Minimal: Deleted tasks add ~50 bytes each (flags + timestamp)
- Automatically cleaned after 30 days
- Typical user impact: < 10KB even with heavy usage

### Performance
- Filtering adds O(n) operation to render (negligible for typical kanban usage)
- Cleanup runs once per day (minimal CPU impact)
- Sync remains efficient with Map-based merging

## Testing Recommendations

1. **Delete on Device A**: Verify it disappears from Device B after sync
2. **Offline Deletion**: Delete while offline, verify it syncs when back online  
3. **Undo**: Test undo functionality within 5-second window
4. **Cleanup**: Manually test by setting a task's `deletedAt` to 31 days ago
5. **Conflict Resolution**: Delete on A, edit on B (offline), then sync both

## Future Enhancements (Optional)

1. **Trash/Archive Feature**: Show deleted items in a "trash" view
2. **Configurable Retention**: Allow user to set cleanup period
3. **Bulk Cleanup**: Manual "empty trash" button
4. **Sync Indicators**: Show when deletions are being synced
