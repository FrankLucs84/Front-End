
# 📘 Guida XML — Personalizzazione di Form e Campi nel Portale CRM

Questa guida illustra come leggere e modificare file XML per personalizzare le viste (`<View>`) e i filtri (`<FilterAreas>`) di form relativi a oggetti come i **Tickets**, in un contesto di portale CRM (es. PAT CRM).

---

## 📂 1. Struttura Generale del File XML

```xml
<Objects xmlns="urn:PAT.CRM.Portal.PortalViews" base="WSCViews_TP_Base.XML">
  <Object type="Tickets" textSearchField="Subject">
    <Views>
      <View id="Default" desc="#WSC_Tickets#"> ... </View>
    </Views>
  </Object>
</Objects>
```

### 🔍 Elementi principali:
- `Object`: rappresenta un'entità (es. Tickets, Orders).
- `View`: definisce la struttura della griglia o form da visualizzare.
- `FilterAreas`: area contenente i filtri applicabili.

---

## 🛠️ 2. Aggiungere o Spostare un Campo nel Filtro

I filtri sono strutturati in `Sections` e `Items`:

```xml
<FilterArea id="default" ...>
  <Sections>
    <Section id="default">
      <Items>
        <Control id="DateFromFilter" field="Date" ... row="0" col="0" />
        <Control id="StatusFilter" field="TicketStatus.Type" ... row="0" col="2" />
      </Items>
    </Section>
  </Sections>
</FilterArea>
```

### 🧩 Spostare un campo:
Modificare gli attributi `row` e `col` del campo `<Control>` per riposizionarlo nella griglia.

### 🆕 Aggiungere un nuovo campo:
```xml
<Control id="CustomerFilter" field="Customer.Name" desc="#WSC_Customer#" type="Auto" row="2" col="0" />
```

---

## 🖼️ 3. Personalizzare le Colonne della Griglia

Le colonne della griglia sono definite dentro `<Columns>`:

```xml
<Columns>
  <Column field="ID" desc="#WSC_ID#" width="130" primary="true" />
  <Column field="Subject" desc="#WSC_Subject#" width="-1">
    <Template id="CP_View_Entity_Ticket_Subject" root="Object" />
  </Column>
</Columns>
```

### 🔄 Per spostare una colonna:
Modifica l'ordine dei tag `<Column>` nel file XML.

### ➕ Per aggiungerne una nuova:
```xml
<Column field="Priority" desc="#WSC_Priority#" width="100" />
```

---

## ⚙️ 4. Attributi Utili

| Attributo | Descrizione |
|----------|-------------|
| `field` | Nome del campo legato al database |
| `desc` | Etichetta del campo (può usare chiavi internazionalizzate) |
| `type` | Tipo di controllo: `Auto`, `ComboBox`, `TextBox`, ecc. |
| `visible` | "1" per visibile, "0" per nascosto |
| `row`, `col`, `colspan` | Posizionamento nel layout grid del filtro |

---

## 🧪 5. Consigli

- Assicurati che gli `id` dei controlli siano univoci.
- Se l'oggetto eredita da una `base`, sovrascrivi solo i nodi necessari.
- Utilizza i commenti `<!-- ... -->` per documentare modifiche.

---

## 📁 Esempio Completo di Filtro Personalizzato

```xml
<Control id="SiteFilter" field="AccountID" filterOperator="eq"
         desc="#WSC_Account#" type="Auto" row="1" col="1" />
```

---

## 📎 Riferimenti

- [PAT CRM Portal Documentation](https://patcrm.docs.example) *(se disponibile)*
- XML Schema e namespace: `urn:PAT.CRM.Portal.PortalViews`
