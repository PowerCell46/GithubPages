class: center, middle

# Мобилни ГИС

.center[
  <img src="./images/TitleImage.png" alt="Title image"
       style="max-width:55%; max-height:45vh; width:auto; height:auto; object-fit:contain; display:block; margin:0 auto;">
]

---
## 1. Какво е Mobile GIS?
* **Дефиниция:** Комбинация от софтуер, хардуер и GPS технология за работа с пространствени данни директно на терен.
* **Основна цел:** Пренасяне на мощта на настолните ГИС системи в мобилното устройство (смартфон или таблет).

.center[
  <img src="./images/PerplexityMobileGis.png" alt="Perplexity mobile GIS"
       style="max-width:55%; max-height:45vh; width:auto; height:auto; object-fit:contain; display:block; margin:0 auto;">
]

---
## 3. Подготовка на данните (ArcGIS Online)
* **Създаване на слоеве (Layers):** Дефиниране на векторни слоеве (точки, линии, полигони) според нуждите на проекта.
* **Структуриране на атрибути:** Добавяне на специфични колони в атрибутивната таблица за прецизно събиране на метаданни.
* **Домейни и списъци:** Настройване на падащи менюта за по-бързо и безгрешно въвеждане на информация на терен.

---
## 4. Конфигуриране на Web Map
* **Интеграция:** Обединяване на всички подготвени слоеве в обща уеб карта.
* **Стилове и симвология:** Настройване на визуалното представяне на обектите за по-добра четивност.
* **Офлайн настройки:** Подготовка на картата за работа в зони без достъп до интернет.

---
## 5. Работа на терен (Field Collection)
* **Мобилен достъп:** Използване на ArcGIS Field Maps за достъп до уеб картата през смартфон или таблет.
* **Заснемане в реално време:** Геопозициониране и попълване на атрибутните данни за всеки обект директно на място.
* **Мултимедия:** Прикачване на снимки и документи към събраните геоданни.

---
## 6. Визуализация: ArcGIS Experience Builder
* **Интерактивен дизайн:** Превръщане на събраните данни в професионално уеб приложение.
* **Функционалност:** Добавяне на уиджети за търсене, филтриране и анализ на резултатите.
* **Достъпност:** Възможност за споделяне на крайния резултат с крайни потребители или вземащи решения лица.

---
## 7. Предимства на използвания работен процес
* **Единен източник на истина:** Данните се обновяват централизирано в ArcGIS Online.
* **Автоматизация:** Пътят от терена до уеб приложението е максимално съкратен.
* **User Experience:** Experience Builder позволява персонализиране на интерфейса спрямо нуждите на потребителя.то

---

.center[
  <img src="./images/holeSizes.png" alt="Hole sizes"
       style="max-width:55%; max-height:45vh; width:auto; height:auto; object-fit:contain; display:block; margin:0 auto;">
]

```python
hole_sizes_data = { "Small / Малка": 5, "Medium / Средна": 5, "Large / Голяма": 3 }

hole_types = [key for key in hole_sizes_data.keys()]
hole_values = np.array([val for val in hole_sizes_data.values()])
total_holes = hole_values.sum()

fig, ax = plt.subplots(figsize=(8, 5))
colors = [COLORS['success'], COLORS['warning'], COLORS['danger']]
bars = ax.bar(hole_types, hole_values, color=colors, edgecolor='white', linewidth=1.5)

ax.set_xlabel('Категория размер', fontsize=12)
ax.set_ylabel('Брой случаи', fontsize=12)
ax.set_title('Разпределение на дупките по размер', pad=15)
ax.set_ylim(0, max(hole_values) + 1.5)

ax.annotate(f'Общо: {total_holes} дупки', xy=(0.98, 0.95), xycoords='axes fraction', ha='right', va='top', fontsize=10, style='italic', bbox=dict(boxstyle='round,pad=0.3', facecolor='#ECF0F1', edgecolor='none'))

plt.tight_layout()
plt.show()
```

---

.center[
  <img src="./images/dangerLevels.png" alt="Danger levels"
       style="max-width:55%; max-height:45vh; width:auto; height:auto; object-fit:contain; display:block; margin:0 auto;">
]

```python
danger_levels_data = { "Много ниско": 5, "Ниско": 3, 
	"Средно": 3, "Високо": 1, "Много високо": 1 }

danger_types = [key for key in danger_levels_data.keys()]
danger_values = np.array([val for val in danger_levels_data.values()])
total_danger = danger_values.sum()

danger_colors = ['#27AE60', '#2ECC71', '#F1C40F', '#E67E22', '#E74C3C']

fig, ax = plt.subplots(figsize=(10, 5))
bars = ax.bar(danger_types, danger_values, color=danger_colors, edgecolor='white', linewidth=1.5)

ax.set_xlabel('Ниво на опасност', fontsize=12)
ax.set_ylabel('Брой случаи', fontsize=12)
ax.set_title('Класификация на инфраструктурни опасности по ниво', pad=15)
ax.set_ylim(0, max(danger_values) + 1.2)

low_risk = ((danger_values[0] + danger_values[1]) / total_danger) * 100
ax.annotate(f'{low_risk:.1f}% Low Risk Cases', xy=(0.02, 0.95), xycoords='axes fraction', ha='left', va='top', fontsize=10, style='italic', color=COLORS['success'], bbox=dict(boxstyle='round,pad=0.3', facecolor='#E8F8F5', edgecolor='none'))

plt.tight_layout()
plt.show()
```

---

.center[
  <img src="./images/roadTypes.png" alt="Road types"
       style="max-width:55%; max-height:45vh; width:auto; height:auto; object-fit:contain; display:block; margin:0 auto;">
]

```python
road_types_data = { "Главен път": 14, "Второстепенен път": 0,
    "Булевард": 0, "Улица": 0 }

road_names = [key for key in road_types_data.keys()]
road_values = np.array([val for val in road_types_data.values()])
total_roads = road_values.sum()

fig, ax = plt.subplots(figsize=(10, 5))
colors = [COLORS['accent'] if v > 0 else COLORS['light'] for v in road_values]
bars = ax.barh(road_names, road_values, color=colors, edgecolor='white', linewidth=1.5, height=0.6)

ax.set_xlabel('Брой случаи', fontsize=12)
ax.set_ylabel('Класификация на пътя', fontsize=12)
ax.set_title('Инфраструктурни проблеми по тип път', pad=15)
ax.set_xlim(0, max(road_values) + 3)

ax.annotate(f'100% on Main Roads\n(n={total_roads})', xy=(0.98, 0.95), xycoords='axes fraction', ha='right', va='top', fontsize=10, style='italic', bbox=dict(boxstyle='round,pad=0.3', facecolor='#EBF5FB', edgecolor='none'))

plt.tight_layout()
plt.show()
```

---

.center[
  <img src="./images/lightPoleWorkingStatus.png" alt="Lightpoles working statuses"
       style="max-width:55%; max-height:45vh; width:auto; height:auto; object-fit:contain; display:block; margin:0 auto;">
]

```python
lightpole_working_statuses_data = {
    "Не работи": 10,
    "Работи": 7,
    "Частично работи": 2
}

lightpole_statuses = [key for key in lightpole_working_statuses_data.keys()]
lightpole_values = np.array([val for val in lightpole_working_statuses_data.values()])
total_poles = lightpole_values.sum()

status_colors = [COLORS['danger'], COLORS['success'], COLORS['warning']]

fig, ax = plt.subplots(figsize=(10, 5))
bars = ax.barh(lightpole_statuses, lightpole_values, color=status_colors, edgecolor='white', linewidth=1.5, height=0.6)

ax.set_xlabel('Брой осветителни стълбове', fontsize=12)
ax.set_ylabel('Оперативен статус', fontsize=12)
ax.set_title('Оперативен статус на уличното осветление', pad=15)
ax.set_xlim(0, max(lightpole_values) + 3)

non_functional = ((lightpole_values[0]) / total_poles) * 100
ax.annotate(f'{non_functional:.1f}% изискват внимание', xy=(0.98, 0.05), xycoords='axes fraction', ha='right', va='bottom', fontsize=10, style='italic', color=COLORS['danger'], bbox=dict(boxstyle='round,pad=0.3', facecolor='#FDEDEC', edgecolor='none'))

plt.tight_layout()
plt.show()
```

---

.center[
  <img src="./images/lightpolesConditionStatuses.png" alt="Lightpoles condition statuses"
       style="max-width:55%; max-height:45vh; width:auto; height:auto; object-fit:contain; display:block; margin:0 auto;">
]

```python
pole_conditions_data = { "Добро": 16, "Средно": 2, "Лошо": 0 }

pole_condition_types = list(pole_conditions_data.keys())
pole_condition_values = np.array(list(pole_conditions_data.values()))
total_condition = pole_condition_values.sum()

condition_colors = [COLORS['success'], COLORS['warning'], COLORS['danger']]

fig, ax = plt.subplots(figsize=(8, 5))
bars = ax.bar(pole_condition_types, pole_condition_values, color=condition_colors, edgecolor='white', linewidth=1.5)

ax.set_xlabel('Физическо състояние', fontsize=12)
ax.set_ylabel('Брой стълбове', fontsize=12)
ax.set_title('Оценка на физическото състояние на стълбовете', pad=15)
ax.set_ylim(0, max(pole_condition_values) + 3)

good_condition = (pole_condition_values[0] / total_condition) * 100
ax.annotate(f'{good_condition:.1f}% в добро състояние', xy=(0.98, 0.95), xycoords='axes fraction', ha='right', va='top', fontsize=10, style='italic', color=COLORS['success'], bbox=dict(boxstyle='round,pad=0.3', facecolor='#E8F8F5', edgecolor='none'))

plt.tight_layout()
plt.show()
```
