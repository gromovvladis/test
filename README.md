# superCalc(5)(2) #7

**1. Решение с () в конце**
    
    def superCalc(initial_value):
        total = initial_value
    
        def wrapper(next_value=None):
            nonlocal total
            if next_value is None:
                return total
            total += next_value
            return wrapper
    
        return wrapper


**2. Решение через декоратор, который обнуляет total при получении строкового значения**

    class Decorator:
        def __init__(self, func):
            self.func = func
            self.total = 0
    
        def __call__(self, next_value=None):
            if next_value is None:
                return self.total
            self.total += next_value
            return self.func(next_value)
    
        def __repr__(self):
            rept = str(self.total)
            self._reset_total()
            return rept
    
        def _reset_total(self):
            self.total = 0

    @Decorator
    def superCalc(num):
        return superCalc
