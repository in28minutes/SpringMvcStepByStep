#Complete Reference : 
http://docs.spring.io/spring/docs/current/spring-framework-reference/html/mvc.html

##Architecture Diagram
http://docs.spring.io/spring/docs/current/spring-framework-reference/html/images/mvc.png

##Dispatcher Servlet
- Dispatches requests to handlers, with configurable handler mappings
- View Resolution
- Locale, time zone and theme resolution 
- Support for uploading files.

##Flexible Data Binding
- Any POJO can be used as a command or form backing object
- Highly Flexible Data Binding. Databinding Errors do not throw exceptions. They only cause validation errors.

##Flexible View Resolution
Controller can either
- Return a View
- Return a View or Model
- Write to response stream directly

##Flexible Controller Methods

###Accepting Variety of Parameters
- Request or response objects : ServletRequest or HttpServletRequest.
- Session object (Servlet API): of type HttpSession. 
- Other Options: http://docs.spring.io/spring/docs/current/spring-framework-reference/html/mvc.html#mvc-ann-methods

###Support Multiple Return Types
- A ModelAndView object
- A Model object

##@ModelAttribute 
###Methods
- Indicates the purpose of that method is to add one or more model attributes.
- Invoked before @RequestMapping methods.
- Used to fill the model with commonly needed attributes 
  - Drop down values for form
  - Command or Form Backing Objects

###Method Argument
- To automatically add/retrieve value from Model
- It can be stored in session as well using @SessionAttributes.


##Validation
###Automatic
@Valid annotation
###Customized
You can also invoke validation using your own custom validator 
```
@RequestMapping(path = "/something", method = RequestMethod.POST)
public String processSubmit(@ModelAttribute("todo") Pet Todo, BindingResult result) {
    new TodoValidator().validate(todo, result);
    if (result.hasErrors()) {
        return "todo";
    }
    // ...
}
```

##@ControllerAdvice

- Can contain @ExceptionHandler, @InitBinder, and @ModelAttribute annotated methods
- These methods will apply to @RequestMapping methods across all controller hierarchies

##Hibernate Validator : JSR 349 Reference Implementation
For more information refer http://docs.jboss.org/hibernate/validator/5.0/reference/en-US/html_single/#validator-defineconstraints-spec

