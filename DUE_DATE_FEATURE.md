# Slutdatum-funktion (Due Date Feature)

## Översikt
Nu kan du lägga till slutdatum på dina uppgifter och få påminnelser när de närmar sig eller passerar förfallodatumet.

## Funktioner

### ✅ Slutdatum på uppgifter
- Lägg till valfritt slutdatum när du skapar eller redigerar uppgifter
- Datum visas på uppgiftskorten med 📅 ikon
- Formaterat i svenskt datumformat (ÅÅÅÅ-MM-DD)

### 🎨 Visuella indikatorer

**Försenad uppgift (Röd):**
- Röd bakgrund och ram
- Badge: "Försenad"
- För uppgifter som passerat slutdatum

**Idag (Gul):**
- Gul/orange bakgrund och ram
- Badge: "Idag"
- För uppgifter som ska slutföras idag

**Snart (Gul badge):**
- Badge: "Snart"
- För uppgifter inom 3 dagar
- Ingen speciell färgkodning på kortet

### 🔔 Notifikationer

**Webbläsar-notifikationer:**
- Begär tillstånd automatiskt vid första användning
- Notifikation vid försenade uppgifter
- Notifikation för uppgifter som ska göras idag
- Kontrollerar automatiskt varje timme

**Exempel på notifikationer:**
- "Försenade uppgifter: Du har 2 försenade uppgifter!"
- "Uppgifter att göra idag: Du har 1 uppgift som ska slutföras idag."

## Hur man använder

### Lägga till slutdatum på ny uppgift
1. Klicka på **"➕ Lägg till"**
2. Fyll i rubrik och beskrivning
3. Klicka på **slutdatum-fältet** och välj ett datum
4. Klicka **"Lägg till"**

### Lägga till slutdatum på befintlig uppgift
1. Klicka på **⋮** på uppgiften
2. Välj **"✏️ Redigera"**
3. Välj ett datum i slutdatum-fältet
4. Klicka **"Spara"**

### Ta bort slutdatum
1. Redigera uppgiften
2. Rensa slutdatum-fältet (lämna tomt)
3. Spara

## Tekniska detaljer

### Datastruktur
Varje uppgift har nu ett valfritt `dueDate` fält:
```javascript
{
  id: "abc123",
  headline: "Min uppgift",
  text: "Beskrivning",
  dueDate: "2025-11-01",  // Valfritt, format: YYYY-MM-DD
  created: 1234567890
}
```

### Datumberäkning
- **Försenad**: `dueDate < idag`
- **Idag**: `dueDate === idag`
- **Snart**: `dueDate inom 3 dagar`

### Notifikationer
- Kontrollerar vid sidladdning (efter 2 sekunder)
- Kontrollerar automatiskt varje timme
- Endast för uppgifter i "Att göra" och "Pågår"
- Uppgifter i "Klart" ignoreras

### Browser-stöd
- Notifikationer: Chrome, Firefox, Edge, Safari
- Datumväljare: Alla moderna webbläsare
- Kräver användarens tillstånd för notifikationer

## Sekretess

- Notifikationer visas endast lokalt på din enhet
- Inga externa servrar kontaktas för notifikationer
- Slutdatum synkas med Firebase om du är inloggad
- Data lagras säkert i din webbläsare och/eller Google-konto

## Tips

💡 **Använd slutdatum strategiskt:**
- Lägg endast till datum på uppgifter som verkligen har en deadline
- För färre notifikationer, använd slutdatum sparsamt
- Flytta slutförda uppgifter till "Klart" för att undvika notifikationer

💡 **Notifikationstillstånd:**
- Om du inte får notifikationer, kolla webbläsarens inställningar
- Du kan alltid se visuella indikatorer även utan notifikationer
- Notifikationer kan stängas av i webbläsarens inställningar

💡 **Sortering:**
- Uppgifter sorteras inte automatiskt efter datum
- Använd drag & drop för att organisera efter prioritet
- Försenade uppgifter är lätta att hitta tack vare röd färg
