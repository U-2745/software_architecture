# Лабораторная работа №6
**Использование шаблонов проектирования**

## Шаблоны проектирования

### Порождающие шаблоны

#### 1. Строитель
**Назначение:**
- процесс создания нового объекта не должен зависеть от того, из каких частей он состоит и от связей этих объектов
- нужно обеспечить получение различных вариаций объекта в процессе его создания
  
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

![prototype](https://github.com/U-2745/software_architecture/assets/78296925/e6bc3125-7186-429a-a8ec-c12163b7ac12)

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

#### 3. Одиночка
**Назначение:**

- когда возникает необходимость в глобальных переменных или объектах с ограниченным числом экземпляров
  
**UML-диаграмма**

![singleton](https://github.com/U-2745/software_architecture/assets/78296925/bf3cdd9d-8366-44b5-9dc3-176faea82845)

**Код**
```
public sealed class Normalizer
{
   private static volatile Normalizer instance;
   private static object syncRoot = new Object();

   private Normalizer() {}

   public static Normalizer Instance
   {
      get 
      {
         if (instance == null) 
         {
            lock (syncRoot) 
            {
               if (instance == null) 
                  instance = new Normalizer();
            }
         }

         return instance;
      }
   }
}
```

### Структурные шаблоны

#### 1. Мост
**Назначение:**
- когда нужно избежать постоянной привязки абстракции к реализации
- когда изменения в абстракции не должно привести к изменениям в реализации
  
**UML-диаграмма**

![bridge](https://github.com/U-2745/software_architecture/assets/78296925/5018a0a9-5b97-45cd-91bc-56eb3af45b6c)

**Код**
```
// абстракция
abstract class Definer
{
    protected ParametersDefiner parametersDefiner;
    public ParametersDefiner ParametersDefiner
    {
        set { parametersDefiner = value; }
    }
    public Definer(ParametersDefiner paramdef)
    {
        parametersDefiner = paramdef;
    }
    public virtual void ComplectDefiner()
    {
        parametersDefiner.ComplectParamsDefiner();
    }
}

// имплементор
abstract class ParametersDefiner
{
    public abstract void ComplectParamsDefiner();
}

// уточнённая абстракция
class ConDefiner : Definer
{
    public ConDefiner(ParametersDefiner paramdef) : base(paramdef) { }
    public override void ComplectConDefiner() { }
}

// 1 реализация, наследованная от имплементатора
class ShapesDefiner : ParametersDefiner
{
    public override void ComplectParamsDefiner() { }
}
 
// 2 реализация, наследованная от имплементатора
class ColorsDefiner : ParametersDefiner
{
    public override void ComplectParamsDefiner() { }
}
```

#### 2. Декоратор
**Назначение:**
- когда надо динамически добавлять к объекту новые функциональные возможности
- когда применение наследования неприемлемо. 
  
**UML-диаграмма**

![decorator](https://github.com/U-2745/software_architecture/assets/78296925/bcc5d4aa-a060-40da-b58b-324867048f83)

**Код**
```
// компонент
abstract class InputAnalyzer
{
    public abstract void Analyze();
}
// конкретный компонент
class PolarityAnalyzer : InputAnalyzer
{
    public override void Analyze() { }
}
// декоратор
abstract class AnalyzerDecorator : InputAnalyzer
{
    protected InputAnalyzer analyzer;
 
    public void SetAnalyzer(InputAnalyzer analyzer)
    {
        this.analyzer = analyzer;
    }
 
    public override void Analyze()
    {
        if (analyzer != null)
            analyzer.Analyze();
    }
}
// дополнительная функциональность 1, расширяющая PolarityAnalyzer
class QuantityAnalyzer : PolarityAnalyzer
{
    public override void Analyze()
    {
        base.Analyze();
    }
}
// дополнительная функциональность 2, расширяющая PolarityAnalyzer
class QualityAnalyzer : PolarityAnalyzer
{
    public override void Analyze()
    {
        base.Analyze();
    }
}
```

#### 3. Фасад
**Назначение:**
- когда нужно упростить работу со сложной системой
- когда надо уменьшить количество зависимостей между клиентом и сложной системой
- когда нужно определить подсистемы компонентов в сложной системе.
  
**UML-диаграмма**

![facade](https://github.com/U-2745/software_architecture/assets/78296925/624be1a4-fba7-461b-a2ac-e9fcd4a032d1)

**Код**
```
//подсистема 1
class InputValidator
{
    public void ValidateInput() { }
}
//подсистема 2
class InputNormalizer
{
    public void NormalizeInput() { }
}
//подсистема 3
class InputAnalyzer
{
    public void AnalyzeInput() { }
}
//подсистема 4
class OutputParametersDefiner
{
    public void DefineOutputParameters() { }
}
//подсистема 5
class OutputGenerator
{
    public void GenerateOutput() { }
}
 
public class GenerativeModuleFacade
{
    InputValidator inputValidator;
    InputNormalizer inputNormalizer;
    InputAnalyzer inputAnalyzer;
    OutputParametersDefiner outputParametersDefiner;
    OutputGenerator outputGenerator;
 
    public Facade(InputValidator inputValidator, InputNormalizer inputNormalizer, InputAnalyzer inputAnalyzer, OutputParametersDefiner outputParametersDefiner,
        OutputGenerator outputGenerator)
    {
        InputValidator = inputValidator;
        InputNormalizer = inputNormalizer;
        InputAnalyzer = inputAnalyzer;
        OutputParametersDefiner = outputParametersDefiner;
        OutputGenerator = outputGenerator;
    }
    public void PrepareInput()
    {
        inputValidator.ValidateInput();
        inputNormalizer.NormalizeInput();
        inputAnalyzer.AnalyzeInput();
    }
    public void AnalyzeInput()
    {
        outputParametersDefiner.DefineOutputParameters();
        outputGenerator.GenerateOutput();
    }
}
```


