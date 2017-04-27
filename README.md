# BuckleScript FFI cheatsheet

## Basic

### [bs.val](https://bloomberg.github.io/bucklescript/Manual.html#_binding_to_global_value_bs_val)
```ml
(* ml *)
external f : 'a -> 'b -> 'ret = "" [@@bs.val]

let ret = f a b
```
```js
// js
var ret = f(a, b);
```

### [bs.get](https://bloomberg.github.io/bucklescript/Manual.html#_binding_to_getter_setter_bs_get_bs_set)
```ml
(* ml *)
external f : 'self -> 'ret = "" [@@bs.get]

let ret = f self
```
```js
// js
var ret = self.f;
```

### [bs.set](https://bloomberg.github.io/bucklescript/Manual.html#_binding_to_getter_setter_bs_get_bs_set)
```ml
(* ml *)
external f : 'self -> 'a -> 'ret = "" [@@bs.set]

let ret = f self a
```
```js
// js
var ret = self.f = a;
```

### [bs.send](https://bloomberg.github.io/bucklescript/Manual.html#_binding_to_method_bs_send_bs_send_pipe)
```ml
(* ml *)
external f : 'self -> 'a -> 'b -> 'ret = "" [@@bs.send]

let ret = f self a b
```
```js
// js
var ret = self.f(a, b);
```

### [bs.send.pipe](https://bloomberg.github.io/bucklescript/Manual.html#_binding_to_method_bs_send_bs_send_pipe)
```ml
(* ml *)
external f : 'a -> 'b -> 'ret = "" [@@bs.send.pipe: 'self]

let ret = f a b self
(* or *)
let ret = self |> f a b
```
```js
// js
var ret = self.f(a, b);
```

### [bs.new](https://bloomberg.github.io/bucklescript/Manual.html#_binding_to_javascript_constructor_bs_new)
```ml
(* ml *)
external f : unit -> 'ret = "" [@@bs.new]

let ret = f ()
```
```js
// js
var ret = new f();
```

### [bs.module](https://bloomberg.github.io/bucklescript/Manual.html#_binding_to_a_value_from_a_module_bs_module)
```ml
(* ml *)
external f : unit -> unit = "" [@@bs.module "m"]

let _ = f ()
```
```js
// js
var m = require('m');
m.f();
```

### [bs.get_index](https://bloomberg.github.io/bucklescript/Manual.html#_binding_to_dynamic_key_access_set_bs_set_index_bs_get_index)
```ml
(* ml *)
external f : 'self -> 'key -> 'ret = "" [@@bs.get_index]

let ret = f self key
```
```js
// js
var ret = self[key];
```

### [bs.set_index](https://bloomberg.github.io/bucklescript/Manual.html#_binding_to_dynamic_key_access_set_bs_set_index_bs_get_index)
```ml
(* ml *)
external f : 'self -> 'key -> 'a -> 'ret = "" [@@bs.set_index]

let ret = f self key a
```
```js
// js
var ret = self[key] = a;
```


## Advanced

### [bs.splice](https://bloomberg.github.io/bucklescript/Manual.html#_splice_calling_convention_bs_splice)
```ml
(* ml *)
external f : 'a -> 'b array -> 'ret = "" [@@bs.val] [@@bs.splice]

let ret = f a [|b1; b2; b3|]
```
```js
// js
var ret = f(a, b1, b2, b3);
```

### [bs.scope](https://bloomberg.github.io/bucklescript/Manual.html#_scoped_values_bs_scope_since_1_7_2)
```ml
(* ml *)
external f : unit -> unit = "" [@@bs.val] [@@bs.scope "a", "b"]

let _ = f ()
```
```js
// js
a.b.f();
```

### [bs.return](https://bloomberg.github.io/bucklescript/Manual.html#_return_value_checking_since_1_5_1)

### [bs.obj](https://bloomberg.github.io/bucklescript/Manual.html#_create_js_objects_using_external)

### [bs.as](https://bloomberg.github.io/bucklescript/Manual.html#_fixed_arguments)
```ml
(* ml *)
external f : 'a -> _ [@bs.as "b"] -> 'c -> unit = "" [@@bs.val]

let _ = f a c
```
```js
// js
f(a, "b", c);
```

### [bs.string](https://bloomberg.github.io/bucklescript/Manual.html#_using_polymorphic_variant_to_model_enums_and_string_types)
```ml
(* ml *)
external f : ([`a] [@bs.string]) -> unit = "" [@@bs.val]

let _ = f `a
```
```js
// js
f("a");
```

### [bs.int](https://bloomberg.github.io/bucklescript/Manual.html#_using_polymorphic_variant_to_model_enums_and_string_types)
```ml
(* ml *)
external f : ([`a] [@bs.int]) -> unit = "" [@@bs.val]

let _ = f `a
```
```js
// js
f(0);
```

### [bs.ignore](https://bloomberg.github.io/bucklescript/Manual.html#_phantom_arguments_and_ad_hoc_polymorphism)
```ml
(* ml *)
external f : 'a -> 'b [@bs.ignore] -> 'c -> unit = "" [@@bs.val]

let _ = f a b c
```
```js
// js
f(a, c);
```

### [bs](https://bloomberg.github.io/bucklescript/Manual.html#__bs_for_explicit_uncurried_callback)
### [bs.uncurry](https://bloomberg.github.io/bucklescript/Manual.html#__bs_uncurry_for_implicit_uncurried_callback_since_1_5_0)
### [bs.this](https://bloomberg.github.io/bucklescript/Manual.html#_bindings_to_code_this_code_based_callbacks_bs_this)
### [bs.open](https://bloomberg.github.io/bucklescript/Manual.html#__code_bs_open_code_type_safe_external_data_source_handling_since_1_7_0)

## Extensions

### [bs.re](https://bloomberg.github.io/bucklescript/Manual.html#_regex_support)
### [bs.obj](https://bloomberg.github.io/bucklescript/Manual.html#_create_js_objects_using_bs_obj)
### [bs.raw](https://bloomberg.github.io/bucklescript/Manual.html#_embedding_raw_js_code_as_statements)
### [bs.debugger](https://bloomberg.github.io/bucklescript/Manual.html#_debugger_support)
### [bs.external](https://bloomberg.github.io/bucklescript/Manual.html#_detect_global_variable_existence_code_bs_external_code_since_1_5_1)
### [bs.node](https://bloomberg.github.io/bucklescript/Manual.html#_binding_to_nodejs_special_variables_bs_node)

## JS Objects

### [Js.t](https://bloomberg.github.io/bucklescript/Manual.html#_binding_to_js_objects)
### [##](https://bloomberg.github.io/bucklescript/Manual.html#_binding_to_js_objects)
### [class type ... end \[@bs\]](https://bloomberg.github.io/bucklescript/Manual.html#_complex_object_type)
### [#=](https://bloomberg.github.io/bucklescript/Manual.html#_how_to_consume_js_property_and_methods)
### [bs.get](https://bloomberg.github.io/bucklescript/Manual.html#_getter_setter_annotation_to_js_properties)
### [bs.set](https://bloomberg.github.io/bucklescript/Manual.html#_getter_setter_annotation_to_js_properties)
