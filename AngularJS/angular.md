# Angular

## Data Binding

Databinding = Communication.

Data binding is the synchronisation between the model and the view. For example, in 2-way data binding, when data in the model changes, the view reflects the change, and when data in the view changes, the model is updated as well. This happens immediately and automatically, which makes sure that the model and the view are updated at all times.<br><br>

## String Interpolation

String interpolation is the process of evaluiating a string literal containing one or more placeholders, meaning dynamic values can be added to a string.

#### Example:<br>
```
string a = "some text by {{ userName }}";
```
<br>

## Directives

Directives are classes that add additional behaviour to elements in your Angular applications.

#### Example:<br>
```
<p appTurnGreen>Receives a green background!</p>

@Directive({
  selector: '[appTurnGreen]'
})
export class TurnGreenDirective {
  ...
}
```
<br>
