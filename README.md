# 🎰 Многорукие бандиты: от теории к практике

## 📌 О проекте

Этот проект посвящен исследованию и реализации алгоритмов многоруких бандитов (Multi-Armed Bandits) — мощного инструмента для решения задач обучения с подкреплением. В работе реализованы и сравнены четыре ключевых алгоритма:

- 🎲 Random (рандомизированный) — базовая стратегия
- 🎯 ε-Greedy — баланс исследования и эксплуатации
- 📊 UCB (Upper Confidence Bound) — доверительные интервалы
- 🧠 LinUCB (Linear UCB) — контекстно-зависимая версия

Особое внимание уделено применению LinUCB к реальным данным, что демонстрирует практическую ценность алгоритма.

## 🛠️ Реализованные алгоритмы

### 1. Random Agent
```python
class RandomAgent:
    def __init__(self, n_arms, save=True):
        self.n_arms = n_arms
        self.estimations = np.zeros(n_arms) # оценки мат. ожиданий награды для каждой из ручек
        self.N = np.zeros(n_arms) # сколько раз использовали каждую из ручек
        self.save = save # сохранять ли результаты для визуализации
        self.cumulative_rewards = [0]
        self.cumulative_regrets = [0]Простая стратегия, служащая базовой линией для сравнения.
```

### 2. ε-Greedy Agent
```python
class EpsilonGreedyAgent:
    def __init__(self, n_arms, epsilon=0.1, save_rewards=True):
        self.n_arms = n_arms
        self.epsilon = epsilon
        self.estimations = np.zeros(n_arms)
        self.N = np.zeros(n_arms)
        self.save_rewards = save_rewards
        self.cumulative_rewards = [0]
        self.cumulative_regrets = [0]Балансирует между исследованием и эксплуатацией через параметр ε.
```

### 3. UCB Agent
```python
class UCBAgent:
    def __init__(self, n_arms, epsilon=0.3, sigma=1,c=2., save_rewards=True):
        self.n_arms = n_arms
        self.epsilon = epsilon
        self.estimations = np.zeros(n_arms)
        self.N = np.zeros(n_arms)
        self.sigma = sigma
        self.save_rewards = save_rewards
        self.cumulative_rewards = [0]
        self.cumulative_regrets = [0]
        self.total_count = 0 # поддерживаем, сколько всего шагов уже было - необходимо для вычисления доверительного интервала
        self.c = cИспользует доверительные интервалы для интеллектуального исследования.
```

### 4. LinUCB Agent
```python
class LinUCBAgent_new:
    def __init__(self, n_arms=10, context_dim=5, exploration_rate=1.0, save=True):
        """
        :param n_arms: Количество ручек (действий).
        :param context_dim: Размерность контекста.
        :param alpha: Параметр, контролирующий исследование (exploration).
        """
        self.n_arms = n_arms
        self.context_dim = context_dim
        self.exploration_rate = exploration_rate

        self.A = [np.eye(context_dim) for _ in range(n_arms)]  # Матрица A для каждой ручки
        self.b = [np.zeros(context_dim) for _ in range(n_arms)]  # Вектор b для каждой ручки
        self.theta = [np.zeros(context_dim) for _ in range(n_arms)]  # Веса для каждой ручки

        self.save = save
        self.cumulative_rewards = [0]
        self.cumulative_regrets = [0]Контекстно-зависимая версия UCB для работы с реальными данными.
```

## 📈 Ключевые результаты

1. Сравнение алгоритмов:
   - Random: линейный рост сожаления
   - ε-Greedy: сублинейный рост
   - UCB: логарифмический рост
   - LinUCB: лучшие результаты на контекстных данных

2. Применение к реальным данным:
   - Реализована система рекомендаций на основе LinUCB
   - Демонстрация работы с признаками пользователей

## 🚀 Как использовать

1. Клонируйте репозиторий:
git clone https://github.com/Robert-PL-create/multi-armed_bandits.git
2. Запустите Jupyter Notebook:
jupyter notebook multi-armed_bandits.ipynb
## 📚 Зависимости

- Python 3.8+
- NumPy
- Matplotlib
- pandas (для работы с реальными данными)
- tqdm (для прогресс-бара)
- IPython.display

---

💡 Совет: Если Вас заинтересовала задача, подробнее о ней можно почитать в этой книге: https://tor-lattimore.com/downloads/book/book.pdf
