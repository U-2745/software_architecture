# Лабораторная работа №6
**Использование шаблонов проектирования**

## Шаблоны проектирования

### Порождающие шаблоны

#### 1. Строитель
**Назначение:**
- процесс создания нового объекта не должен зависеть от того, из каких частей он состоит и от связей этих объектов
- нужно обеспечить получение различных вариаций объекта в процессе его создания
- 
**UML-диаграмма**
![builder](https://github.com/U-2745/software_architecture/assets/78296925/d30a42cf-39fe-44ef-b4e3-3abf8a7da363)

**Код**
```
 class Shapes
    {
        public Shapes() { // определили формы текста }
    }
  class Colors
    {
        public Colors() { // определили цвета текста }
    }
  
  class Parameters
    {
        public Shapes Shapes;
        public Colors Colors;
    }

// абстрактный класс строителя
 abstract class Former
    {
        public Parameters Parameters;
        public void FillParameters()
        {
            Parameters = new Parameters();
        }
        public Parameters params;
        public abstract void ExtractShapes();
        public abstract void ExtractColors();
    }

// директор
 class Constructor
 {
     public Former Construct(Former Former)
     {
         Former.FillParameters();
         Former.ExtractShapes();
         Former.ExtractColors();
         return Former.Parameters;
     }
 }

// строитель
 class ParamsFormer : Former
    {
        public override void ExtractShapes()
        {
            params.Add(new Shapes());
        }

        public override void ExtractColors()
        {
            params.Add(new Colors());
        }

        public override Parameters GetResult()
        {
            return params;
        }
    }
```

#### 2. Прототип
**Назначение:**

- когда конкретный тип создаваемого объекта должен определяться динамически во время выполнения
- когда нежелательно создание отдельной иерархии классов фабрик для создания объектов-продуктов из параллельной иерархии классов
- когда клонирование объекта предпочтительнее создания и инициализации через конструктор (особенно когда известно, что  объект может принимать небольшое ограниченное число возможных состояний)
  
**UML-диаграмма**
![image](https://github.com/U-2745/software_architecture/assets/78296925/e6bc3125-7186-429a-a8ec-c12163b7ac12)


**Код**
```
// клиент
class Client { // работа с прототипом }

// прототип
abstract class ShapesSample
{
    public int Id { get; private set; }
    ArrayList shapes { get; private set; }
    public ShapesSample(int id)  { this.Id = id; }
    public abstract ShapesSample Clone();
}

// реализация 1
class HardShapes : ShapesSample
{
    public HardShapes(int id) : base(id) { }
    public override ShapesSample Clone()
    {
        return new HardShapes(Id);
    }
}

// реализация 2
class SoftShapes : ShapesSample
{
    public SoftShapes(int id) : base(id) { }
    public override ShapesSample Clone()
    {
        return new SoftShapes(Id);
    }
}

// реализация 3
class NeutralShapes : ShapesSample
{
    public NeutralShapes(int id) : base(id) { }
    public override ShapesSample Clone()
    {
        return new NeutralShapes(Id);
    }
}
```
