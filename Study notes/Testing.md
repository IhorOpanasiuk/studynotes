**Тестування** - це перевірка правильності роботи програми або її компонентів.
Види тестування:
1. Unit Testing - тестування окремих компонентів коду. Зазвичай пишеться розробниками.
2. Integration Testing - перевірка взаємодії різних компонентів. (Може включати роботу з БД і т.п.)
3. System testing - тестування всієї системи в цілому.
4. Acceptance testing - перевірка відповідності бізнес-вимогам. Часно виконується замовником з фокусом на сценарії використання.

Серед бібліотек для написання unit-тестів в .Net часто використовується xUnit.
xUnit.Net - це безкоштовний інструмент з відкритим кодом для модульного тестування в .NET. Ось основні концепції:
```
public class CalculatorTests
{
    [Fact] // Позначає метод як тест
    public void Add_ShouldReturnSum()
    {
        // Arrange
        var calculator = new Calculator();
        
        // Act
        int result = calculator.Add(2, 3);
        
        // Assert
        Assert.Equal(5, result);
    }

    [Theory] // Для параметризованих тестів
    [InlineData(3, 5, 8)]
    [InlineData(-1, 1, 0)]
    public void Add_MultipleInputs_ShouldReturnSum(int a, int b, int expected)
    {
        var calculator = new Calculator();
        int result = calculator.Add(a, b);
        Assert.Equal(expected, result);
    }
}
```
### Ключові особливості xUnit:
- [Fact] - атрибут для простих тестів
- [Theory] - для параметризованих тестів
- Assert клас для перевірки результатів
- Підтримка асинхронного тестування
- Можливість групування тестів
- Гнучка система фільтрації тестів

xUnit також підтримує:
- Налаштування оточення через конструктори та IDisposable
- Спільне використання контексту між тестами
- Паралельне виконання тестів
- Пропуск тестів (Skip)
- Тестові колекції для групування

Ця бібліотека є сучасною альтернативою MSTest та NUnit, і активно використовується в проєктах .NET Core.

# Порівняння фреймворків тестування .NET

| Характеристика                 | NUnit                                     | MSTest                            | xUnit                          |
| ------------------------------ | ----------------------------------------- | --------------------------------- | ------------------------------ |
| **Атрибути тестів**            | `[Test]`                                  | `[TestMethod]`                    | `[Fact]`                       |
| **Параметризовані тести**      | `[TestCase]`                              | `[DataRow]`                       | `[Theory]` + `[InlineData]`    |
| **Ініціалізація тесту**        | `[SetUp]`                                 | `[TestInitialize]`                | Конструктор класу              |
| **Очищення після тесту**       | `[TearDown]`                              | `[TestCleanup]`                   | IDisposable.Dispose()          |
| **Ініціалізація класу**        | `[OneTimeSetUp]`                          | `[ClassInitialize]`               | IClassFixture<T>               |
| **Очищення класу**             | `[OneTimeTearDown]`                       | `[ClassCleanup]`                  | IClassFixture<T>               |
| **Пропуск тесту**              | `[Ignore("причина")]`                     | `[Ignore]`                        | `[Fact(Skip`<br>`="причина")]` |
| **Категорії тестів**           | `[Category("name")]`                      | `[TestCategory`<br>`("name")]`    | `[Trait("Category", "name")]`  |
| **Очікування виключень**       | `[TestCase(typeof`<br>`(Exception))]`     | `[ExpectedException]`             | Assert.Throws<Exception>()     |
| **Паралельне виконання**       | Потребує конфігурації                     | Ні за замовчуванням               | Так за замовчуванням           |
| **Підтримка async/await**      | Так                                       | Так                               | Так                            |
| **Assertion синтаксис**        | Assert.That(actual, Is.EqualTo(expected)) | Assert.AreEqual(expected, actual) | Assert.Equal(expected, actual) |
| **Колекції тестів**            | `[TestFixture]`                           | `[TestClass]`                     | Неявно через клас              |
| **Інтеграція з Visual Studio** | Через розширення                          | Вбудована                         | Через розширення               |
| **Підтримка .NET Core**        | Так                                       | Так                               | Так                            |
| **Розширюваність**             | Висока                                    | Середня                           | Висока                         |


## Додаткові особливості

### NUnit
- Багатий набір assertions
- Гнучка система обмежень (constraints)
- Підтримка декількох платформ
- Великий набір атрибутів для різних сценаріїв
### MSTest
- Найкраща інтеграція з Visual Studio
- Простий у вивченні
- Прямолінійний підхід до тестування
- Добре підходить для початківців
### xUnit
- Сучасний дизайн
- Найкраща підтримка паралелізму
- Менше "магічних" атрибутів
- Використовується командою .NET Core
- Кращі практики вбудовані в дизайн
## Особливості вибору

- Для нових проектів частіше рекомендують xUnit
- Для корпоративних проектів з великою кодовою базою часто використовують NUnit
- MSTest найкраще підходить для команд, які тісно інтегровані з екосистемою Microsoft