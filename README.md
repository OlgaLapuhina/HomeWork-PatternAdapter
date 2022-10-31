## Домашнее задание по теме «Структурные шаблоны. Proxy, Decorator, Adapter»

Задача №1. “Калькулятор” (обязательная)
Описание
В этом задании попрактикуемся с шаблоном Adapter (Адаптер). Ниже вам дан готовый класс калькулятора:

    public class Calculator {
    public Formula newFormula() {
    return new Formula();
    }

    public static enum Operation {
    SUM, SUB, MULT, DIV, POW;
    }

    public static class Formula {
    protected Double a, b, result;

    protected Formula() {}

    public Formula addOperand(double operand) {
      if (a == null) {
        a = operand;
      } else if (b == null) {
        b = operand;
      } else {
        throw new IllegalStateException("Formula is full of operands");
      }
      return this;
    }

    public Formula calculate(Operation op) {
      if (a == null || b == null)
        throw new IllegalStateException("Not enough operands!");
      switch (op) {
        case SUM:
          result = a + b;
          break;
        case SUB:
          result = a - b;
          break;
        case MULT:
          result = a * b;
          break;
        case DIV:
          result = a / b;
          break;
        case POW:
          result = Math.pow(a, b);
          break;
      }
      return this;
    }

    public double result() {
      if (result == null)
        throw new IllegalStateException("Formula is not computed!");
      return result;
    }

Пользователю же нужен другой интерфейс для работы с калькулятором, который он использует в main.
Вам надо написать класс IntsCalculator, который будет имплементировать интерфейс Ints, “под капотом” делая вычисления через класс Calculator.