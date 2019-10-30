# Angular-8-Dynamic-Reactive-Forms-Example
This is a quick example of how to build a dynamic form with validation in Angular 8 using Reactive Forms. The example is a simple order form for selecting the number of tickets to purchase and entering a name and email address for each ticket. All fields are required and email fields must contain a valid email address.

**Form Validation**
Form to validate on submit instead of on field change, this is implemented with a submitted property in the app component that is set to true when the form is submitted for the first time, and reset to false if the reset or clear button is clicked.

The "Buy Tickets" button displays the form values in an alert popup if the form is valid. The "Reset" button resets the form back to it's initial state including the removal of all ticket name & email fields. The "Clear" button clears the values of ticket name & email fields.

Styling of the example is all done with Bootstrap 4.3 CSS.

**Dynamic Reactive Forms App Component**

The app component defines the form fields and validators for the dynamic form using an Angular FormBuilder to create an instance of a FormGroup that is stored in the dynamicForm property. The dynamicForm is then bound to the form in the app template below using the [formGroup] directive.

The dynamic form contains two properties:

numberOfTickets is an Angular FormControl that stores the number of tickets selected. It is bound to the select input in the app component template with the directive formControlName="numberOfTickets".
tickets is an Angular FormArray used to hold an array of form groups (FormGroup) for storing ticket holder details. Each ticket form group contains a FormControl for the name and email of the ticket holder.
The f and t getters are convenience properties to make it easier to access form controls from the template. So for example you can access the numberOfTickets field in the template using f.numberOfTickets instead of dynamicForm.controls.numberOfTickets.

The onChangeTickets() method dynamically adds or removes ticket forms from the tickets form array when the number of tickets selected is increased or decreased.

The onSubmit() method sets the submitted property to true to show validation messages, checks if the form is valid and displays the form values in an alert popup if it is.

The onReset() method resets the submitted property to false to hide validation messages, clears all form values with this.dynamicForm.reset(), and removes ticket name & email fields with this.t.clear().

The onClear() method resets the submitted property to false to hide validation messages, and clears the values of ticket name & email fields with this.t.reset().

**Dynamic Reactive Forms App Template**

The form element uses the [formGroup] directive to bind to the dynamicForm FormGroup in the app component above.

A nested form group with name and email fields is rendered for each ticket by looping over the tickets form array with the Angular *ngFor directive. Each ticket form group is bound to a containing div element with the directive [formGroup]="ticket".

The form binds the form submit event to the onSubmit() handler in the app component using the Angular event binding (ngSubmit)="onSubmit()". Validation messages are displayed only after the user attempts to submit the form for the first time, this is controlled with the submitted property of the app component.

The reset button click event is bound to the onReset() handler in the app component using the Angular event binding (click)="onReset()", and the clear button is bound to the onClear() handler with (click)="onClear()".
