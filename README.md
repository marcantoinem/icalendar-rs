# iCalendar in Rust

A library (far from anything) to generate icalendars
This is still just an early idea, there is nothing implemented,
I haven't even read the full [spec](http://tools.ietf.org/html/rfc5545) yet.

You want to help make this more mature? Please talk to me, Pull Requests and suggestions are very welcome.

## Examples 

```rust
let event = Event::new()
    .summary("test event")
    .description("here I have something really important to do")
    .starts(UTC::now())
    .class(Class::Confidential)
    .ends(UTC::now() + Duration::days(1))
    .append_property(Property::new("TEST", "FOOBAR")
              .add_parameter("IMPORTANCE", "very")
              .add_parameter("DUE", "tomorrow")
              .done())
    .done();

let bday = Event::new()
    .all_day(UTC.ymd(2016, 3, 15))
    .summary("My Birthday")
    .description(
r#"Hey, I'm gonna have a party
BYOB: Bring your own beer.
Hendrik"#
)
    .done();

let todo = Todo::new().summary("Buy some milk").done();


vobject::parse_component(&bday.to_string()).unwrap();
vobject::parse_component(&todo.to_string()).unwrap();
vobject::parse_component(&event.to_string()).unwrap();

let mut calendar = Calendar::new();
calendar.add(event);
calendar.add(todo);
calendar.add(bday);
```
