
# 📘 Guida JavaScript — Visibilità e Obbligatorietà nei Form Dinamici

Questa guida descrive come applicare regole di visibilità e obbligatorietà nei form dinamici, partendo da una struttura JSON di configurazione.

---

## ✅ 1. Mostrare o Nascondere un Campo

```javascript
function toggleVisibility(fieldId, condition) {
  const field = document.getElementById(fieldId);
  field.style.display = condition ? 'block' : 'none';
}
```

### 📌 Esempio:
```javascript
toggleVisibility("P3C11", document.getElementById("P3C10").value !== "");
```

---

## 🔐 2. Rendere un Campo Obbligatorio

```javascript
function setMandatory(fieldId, condition) {
  const field = document.getElementById(fieldId);
  if (condition) {
    field.setAttribute("required", "true");
  } else {
    field.removeAttribute("required");
  }
}
```

### 📌 Esempio:
```javascript
setMandatory("P3C13", document.getElementById("P3C12").checked);
```

---

## 🔄 3. Applicare Regole su Eventi (`change`)

```javascript
document.getElementById("P3C10").addEventListener("change", function() {
  toggleVisibility("P3C11", this.value !== "");
  setMandatory("P3C11", this.value !== "");
});
```

---

## 📊 4. Eseguire Regole da JSON

```javascript
const rules = [
  {
    field: "P6C14",
    dependsOn: "P6C12",
    condition: val => val === "AM/OEM",
    actions: ["visibleIf", "mandatoryIf"]
  }
];

function applyRules() {
  rules.forEach(rule => {
    const trigger = document.getElementById(rule.dependsOn);
    const field = document.getElementById(rule.field);
    const result = rule.condition(trigger.value);

    if (rule.actions.includes("visibleIf")) {
      toggleVisibility(rule.field, result);
    }
    if (rule.actions.includes("mandatoryIf")) {
      setMandatory(rule.field, result);
    }
  });
}

rules.forEach(rule => {
  const trigger = document.getElementById(rule.dependsOn);
  trigger.addEventListener("change", applyRules);
});
```

---

## ⚙️ 5. Operatori Utili

```javascript
const operators = {
  eq: (a, b) => a === b,
  nn: a => a !== null && a !== undefined && a !== ""
};
```
