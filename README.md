## **Анализ распределения возраста пассажиров Титаника по полу и выживаемости**

### **Цель исследования**  
Проверить, различается ли средний возраст среди 4 групп пассажиров:  
1. Выжившие мужчины  
2. Погибшие мужчины  
3. Выжившие женщины  
4. Погибшие женщины  

---

### **Методы и результаты**

#### **1. Предобработка данных**
- Удалены пропуски в столбце `Age`
- Для баланса групп случайно отобрано по 50 пассажиров из каждой категории

#### **2. Проверка нормальности (тест Шапиро-Уилка)**
Все группы имеют нормальное распределение (p-value > 0.05):
```python
men_survived:    p = 0.860  
women_survived:  p = 0.538  
men_non_survived: p = 0.420  
women_non_survived: p = 0.848
```
## **3. Проверка равенства дисперсий (тест Левена)**

```python
# Сравнение выживших мужчин и женщин
levene(men_survived, women_survived)
# Результат: pvalue=0.750 (> 0.05) → дисперсии равны

# Сравнение погибших мужчин и женщин
levene(men_non_survived, women_non_survived)
# Результат: pvalue=0.726 (> 0.05) → дисперсии равны
```
## **4. Сравнение средних значений (T-тест)**

Для сравнения среднего возраста между группами был применен независимый t-тест:

```python
# Сравнение выживших мужчин и женщин
from scipy.stats import ttest_ind
t_stat, p_value = ttest_ind(men_survived, women_survived, equal_var=True)
print(f"Выжившие: t = {t_stat:.3f}, p = {p_value:.3f}")

# Сравнение погибших мужчин и женщин
t_stat, p_value = ttest_ind(men_non_survived, women_non_survived, equal_var=True)
print(f"Погибшие: t = {t_stat:.3f}, p = {p_value:.3f}")
```
# **Итоговые выводы**
Основной результат:

Не найдено статистически значимых различий в возрасте:

Между выжившими мужчинами и женщинами (p = 0.895)
Между погибшими мужчинами и женщинами (p = 0.392)
