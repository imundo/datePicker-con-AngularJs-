Angular Datepicker
==================
![Angular datepicker calendar](http://i.imgur.com/jKfADtA.png)

Angular datepicker is an angularjs directive that generates a datepicker calendar on your input element.

## Requerimientos minimos

AngularJS v1.3+


## Carga de dependencia 

Para ser usada como directiva, debes incluir archivos de angular Datapicker  javascript y ccs  en tu pagina web:
```html
<!DOCTYPE HTML>
<html>
<head>
  <link href="src/css/angular-datepicker.css" rel="stylesheet" type="text/css" />
</head>
<body ng-app="app">
  //.....
  <script src="src/js/angular-datepicker.js"></script>
</body>
</html>
```

## Instalacion

#### Bower

```
$ bower install angularjs-datepicker --save
```
#### Npm

```
$ npm install angularjs-datepicker --save
```

_then load the js files in your html_

### agregar dependencia de modulo
Add the datepicker module dependency

```js
angular.module('app', [
  'datepicker'
 ]);
```

Llama a la directiva donde quieras en tu página html.

```html
<datepicker>
  <input ng-model="date" type="text"/>
</datepicker>
```
>Por defecto, el modelo ng mostrará un objeto de fecha () de Javascript dentro de su entrada, puede usar las opciones a continuación para configurar su formato de fecha preferido para.


## DOC

Option | Type | Default | Description
------------- | ------------- | ------------- | -------------
date-set="" | String | false | Set a default date to show and init datepicker
 |  | | **tip:** _Do not use same scope for ng-model="date" and date-set="{{date}}", this example is wrong._
 |  | | **tip:** _If you want to pass a Date Object inside do like this date-set="{{newDateObject.toString()}}"_
 |  | | **tip:** _Consider that `date-set="{{myDate}}"` equals to `new Date(attr.dateSet)`, be sure the date you pass inside date-set="" is always in a correct ISO format, or adjust it based on the browser locale to avoid problems with that."._
date-format="" | String | String(new Date()) | Set the date format you want to use, see the list [here](https://docs.angularjs.org/api/ng/filter/date)
 |  | | **tip:** _Be always sure to use a recognized format, maybe try first of all to pass it through new Date('...') and see if it's recognized_
date-min-limit="" | String | false | Set a minimum date limit - you can use all the accepted date formats by the javascript `new Date()`
date-max-limit="" | String | false | Set a maximum date limit - you can use all the accepted date formats by the javascript `new Date()`
date-set-hidden="" | String(Boolean) | false | Set the default date to be shown only in calendar and not in the input field
date-disabled-dates="" | String([Date(), Date(), ...]) | false | Disable specific dates using an _Array_ of dates.
date-enabled-dates="" | String([Date(), Date(), ...]) | false | Enable only the specific dates using an _Array_ of dates.
date-disabled-weekdays="" | String(1, 5, ...]) | false | Disable specific weekdays using an _Array_ of weeks number
date-refocus="" | String(Boolean) | false | Set the datepicker to re-focus the input after selecting a date
date-typer="" | String(Boolean) | false | Set the datepicker to update calendar date when user is typing a date, see validation [tips](#date-validation)
date-week-start-day="" | String(Number) | 0 | Set the first day of the week. Must be an integer between 0 (Sunday) and 6 (Saturday). (e.g. 1 for Monday)
datepicker-class="" | String('class1 class2 class3') | false | Set custom class/es for the datepicker calendar
datepicker-append-to="" | String('#id','.classname', 'body') | false | Append the datepicker to #id or  .class element or to body
datepicker-toggle="" | String(Boolean) | true | Set the datepicker to toggle its visibility on focus and blur 
| | | **tip:** Best is to use `pointer-events: none;` on your input if you don't want the user to toggle the calendar visibility.
datepicker-show="" | String | false | Trigger the datepicker visibility, if true datepicker is shown if false it is hidden
 |  | | **tip:** _Do not mix it with datepicker-toggle for a more stable behavior_
datepicker-mobile="" | String | true | Set to `false` to force override of mobile styles. Especially useful for using desktop-style pagination control in mobile apps.

## Optiones
Angular datepicker le permite usar algunas opciones a través de los datos del atributo `attribute` 

#### Títulos personalizados

Puede configurar los títulos para los selectores de mes y año con la **date-year-title=""** y **date-month-title=""** data attributes (default to is _"select month"_ and _"select year"_)

```html
<datepicker date-month-title="selected year">
    <input ng-model="date"/>
</datepicker>

<datepicker date-year-title="selected title">
    <input ng-model="date"/>
</datepicker>
```

#### Destaque el dia de hoy en el calendario
Para resaltar o diseñar el día de hoy en el calendario, use su propia clase de CSS (`._720kb-datepicker-today`) como esto:

```css
._720kb-datepicker-calendar-day._720kb-datepicker-today {
  background:red;
  color:white;
}
```

```html
<datepicker button-prev="<i class='fa fa-arrow-left'></i>" button-next="<i class='fa fa-arrow-right'></i>">
  <input ng-model="date" type="text"/>
</datepicker>
```

#### Títulos de botones personalizados para flechas
También puede configurar los títulos para las flechas izquierda y derecha con ** button-next-title = "" ** para la derecha y ** button-prev-title = "" ** para la izquierda. Por defecto están etiquetados _ "next" _ y _ "prev" _.


```html
<datepicker button-prev-title="previous month">
    <input ng-model="date"/>
</datepicker>

<datepicker button-next-title="next month">
    <input ng-model="date" type="text"/>
</datepicker>
```

####Entrada como grandchild
A veces no se puede colocar la entrada de fecha como primer hijo del selector de fechas. En este caso, puede usar `selector =" "` para apuntar a la clase CSS de la entrada. A continuación el ejemplo con el uso de Twitter Bootstrap y FontAwesome

```html
<datepicker date-format="yyyy-MM-dd" selector="form-control">
    <div class="input-group">
        <input class="form-control" placeholder="Choose a date"/>
        <span class="input-group-addon" style="cursor: pointer">
        <i class="fa fa-lg fa-calendar"></i>
        </span>
    </div>
</datepicker>
```
#### Mostrar y ocultar manualmente datepicker
A veces desea (manualmente / programáticamente) mostrar u ocultar el selector de fecha, esto se puede lograr usando el atributo `datepicker-show`, si` false`, datepicker está oculto, si `true`, datepicker se muestra

```javascript
.controller('TestController', ['$scope', '$interval', function TestController($scope, $interval) {
    $scope.visibility = true;

    $interval(function setInterval() {
      //toggling manually everytime
      $scope.visibility = !$scope.visibility;
    }, 3500);
  }]);
```
```html
  <datepicker ng-controller="TestController" datepicker-show="{{visibility}}">
      <input ng-model="date3" type="text" class="angular-datepicker-input"/>
    </datepicker>
```
_tip: debe usar este atributo junto con `datepicker-toggle =" false ", para un mejor comportamiento estable del datepicker_


#### Entrada como grandchild
A veces no se puede colocar la entrada de fecha como primer hijo del selector de fechas. En este caso puedes usar
 `selector=""` para apuntar a la clase CSS de la entrada. A continuación el ejemplo con el uso de Twitter Bootstrap y FontAwesome


```html
<datepicker date-format="yyyy-MM-dd" selector="form-control">
    <div class="input-group">
        <input class="form-control" placeholder="Choose a date"/>
        <span class="input-group-addon" style="cursor: pointer">
        <i class="fa fa-lg fa-calendar"></i>
        </span>
    </div>
</datepicker>
```
### Tips

#### Validacion de fecha
Si tu necesitas validar una fecha, mientras el usario esta ingresando esta,tu tienes que refererla por`ngModel`.

```html
<div ng-controller="MyCtrl as ctrl">
<input datepicker type="text" ng-model="myDate"/>
</div>
```
Puede mostrar errores de validación simplemente validando el ngModel, como lo haría con cualquier otro tipo de entrada, por ejemplo:
```javascript
.controller('Ctrl', ['$scope', function ($scope) {
  var liveDate;

  $scope.$watch('myDate', function (value) {
    try {
     liveDate = new Date(value);
    } catch(e) {}

    if (!liveDate) {

      $scope.error = "This is not a valid date";
    } else {
      $scope.error = false;
    }
  });
}]);
```

Entonces su html final:
```html
<div ng-controller="MyCtrl as ctrl">
<input type="text" ng-model="myDate" datepicker/>
<div ng-show="ctrl.error">{{ctrl.error}}</div>
</div>
```





