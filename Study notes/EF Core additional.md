## Ключі
З цікавого те, що немає необхідності прописувати в моделей явно foreign key колонки, якщо ми пишемо залежності через fluent API. А в конфігурації достатньо буде просто написати `builder.HasOne(x => x.Friend).WithMany()` і все.

## Міграції
Міграцію можна експортувати як sql-скрипт, для цього треба написати 
``` CLI
dotnet ef migrations script -o script.sql
```
Кожна міграція буде окремою транзакцією.
## Seed
Для заповнення бд даними в конфігурації треба написати `builder.HasData(Entity[])` і передати в метод масив екземплярів.

## Change Tracking

Зміни які ORM побачила але ще не зафіксувала в бд можна прочитати через 
`_dbContext.ChangeTracker.Entries();` який повертаає масив об'єктів EntityEntry.

![[Pasted image 20241228013511.png]]


Не обов'язково для кожної таблиці створювати DbSet. DbSet потрібен для можливості напряму звертатись до таблиці. Таблиця всеодно буде створена в бд якщо є ентіті зв'язана із сутністю із якої зробили DbSet.