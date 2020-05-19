# Параметризация геометрических объектов

В машинном проектировании кривые и поверхности часто используются в качестве каркаса, поверх которого затем надстраивается более сложная геометрия. Чтобы эти базовые геометрические объекты можно было использовать в качестве основы для других объектов, необходимо написать сценарий для извлечения количественных характеристик, таких как положение и ориентация, по всей площади такого объекта. И кривые, и поверхности поддерживают этот процесс, который называется параметризацией.

Представим, что каждой точке на кривой назначен уникальный параметр в диапазоне от 0 до 1. Если мы создаем объект NurbsCurve путем интерполяции или по нескольким управляющим точкам, то первой точке назначается параметр со значением 0, а последней — параметр со значением 1. Заранее узнать, какой именно параметр будет назначен любой из промежуточных точек, невозможно. Эта проблему можно свести к минимуму путем использования нескольких вспомогательных функций. Процесс параметризации поверхностей аналогичен процессу для кривых, за исключением того, что вместо одного параметра назначаются два — u и v. Предположим, что требуется создать поверхность по следующим точкам:

```js
pts = [ [p1, p2, p3],
        [p4, p5, p6],
        [p7, p8, p9] ];
```

В этом случае точке p1 будут назначены параметры u = 0, v = 0, а точке p9 — u = 1, v = 1.

Для определения точек, на основе которых строится кривая, параметризация не слишком эффективна. Ее основное назначение — определение местоположений промежуточных точек, создаваемых конструкторами NurbsCurve и NurbsSurface.

Для работы с кривыми доступен метод *PointAtParameter*, который в качестве входных данных использует один двойной аргумент в диапазоне между 0 и 1 и возвращает объект Point, соответствующий этому параметру. Например, при использовании этого сценария были определены точки с параметрами 0, 0.1, 0.2, 0.3, 0.4, 0.5, 0.6, 0.7, 0.8, 0.9 и 1:

![](images/12-7/GeometricParameterization_01.png)

```js
pts = {};
pts[0] = Point.ByCoordinates(4, 0, 0);
pts[1] = Point.ByCoordinates(6, 0, 1);
pts[2] = Point.ByCoordinates(4, 0, 2);
pts[3] = Point.ByCoordinates(4, 0, 3);
pts[4] = Point.ByCoordinates(4, 0, 4);
pts[5] = Point.ByCoordinates(3, 0, 5);
pts[6] = Point.ByCoordinates(4, 0, 6);

crv = NurbsCurve.ByPoints(pts);

pts_at_param = crv.PointAtParameter(0..1..#11);

// draw Lines to help visualize the points
lines = Line.ByStartPointEndPoint(pts_at_param, 
    Point.ByCoordinates(4, 6, 0));
```

Для работы с поверхностями доступен аналогичный метод *PointAtParameter*, который в качестве входных данных использует два аргумента, а именно параметры u и v созданного объекта Point.

Хотя извлечение отдельных точек кривой или поверхности может быть само по себе полезно, для выполнения многих сценариев требуются определенные геометрические характеристики конкретного параметра, например направление кривой или поверхности. Метод *CoordinateSystemAtParameter* позволяет определить не только положение конкретного параметра кривой или поверхности, но и ориентацию соответствующего объекта CoordinateSystem. Например, следующий сценарий извлекает сведения об ориентации объектов CoordinateSystem относительно поверхности вращения и использует эти сведения для построения отрезков перпендикулярно этой поверхности:

![](images/12-7/GeometricParameterization_02.png)

```js
pts = {};
pts[0] = Point.ByCoordinates(4, 0, 0);
pts[1] = Point.ByCoordinates(3, 0, 1);
pts[2] = Point.ByCoordinates(4, 0, 2);
pts[3] = Point.ByCoordinates(4, 0, 3);
pts[4] = Point.ByCoordinates(4, 0, 4);
pts[5] = Point.ByCoordinates(5, 0, 5);
pts[6] = Point.ByCoordinates(4, 0, 6);
pts[7] = Point.ByCoordinates(4, 0, 7);

crv = NurbsCurve.ByPoints(pts);

axis_origin = Point.ByCoordinates(0, 0, 0);
axis = Vector.ByCoordinates(0, 0, 1);

surf = Surface.ByRevolve(crv, axis_origin, axis, 90,
    140);

cs_array = surf.CoordinateSystemAtParameter(
    (0..1..#7)<1>, (0..1..#7)<2>);

def make_line(cs : CoordinateSystem) { 
	lines_start = cs.Origin;
    lines_end = cs.Origin.Translate(cs.ZAxis, -0.75);
    
    return = Line.ByStartPointEndPoint(lines_start, 
        lines_end);
}

lines = make_line(Flatten(cs_array));
```

Как уже упоминалось, параметризация не всегда выполняется равномерно по всей длине кривой или поверхности. Это значит, что параметр 0.5 не всегда соответствует средней точке, а параметр 0.25 — точке на отметке в одну четвертую длины кривой или поверхности. Чтобы обойти это ограничение, можно воспользоваться дополнительным набором команд параметризации, доступным для объектов Curve. Эти команды позволяют найти точки, расположенные в определенном месте на кривой.
