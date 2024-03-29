## Auto Complete

The EntityFilter filters a property for entities as a dropdown.

It is not recommended to use this filter if the number of possible
entities is possible to become very big. If this is the case, consider
using AutoCompleteEntityFilter instead.

<ReferenceTable
type="auto_complete_entity"
className="Enhavo\Bundle\AppBundle\Filter\Type\AutoCompleteEntityFilter"
>
<template v-slot:options>
    <ReferenceOption name="route" type="text" :required="true"/>,
    <ReferenceOption name="property" type="text" :required="true"/>,
    <ReferenceOption name="label" type="text" :required="true"/>,
    <ReferenceOption name="route_parameters" />
    <ReferenceOption name="minimum_input_length" />
</template>
<template v-slot:inherit>
    <ReferenceOption name="label" />,
    <ReferenceOption name="locale" />,
    <ReferenceOption name="format" />,
    <ReferenceOption name="initial_active" />,
    <ReferenceOption name="initial_value" />,
    <ReferenceOption name="initial_value_arguments" />,
    <ReferenceOption name="initial_value_repository" />,
    <ReferenceOption name="initial_value_choice_label" />,
    <ReferenceOption name="condition" />,
    <ReferenceOption name="width" />,
    <ReferenceOption name="permission" />,
    <ReferenceOption name="component" />
</template>
</ReferenceTable>

### route

**type**: `string`

Route that will be called for the autocomplete search. The route will be
used in the following way:

-   Get-Parameter [q]{.title-ref} will have the search term as a string
-   Get-Parameter [page]{.title-ref} will be an integer representing the
    pagination page
-   Additional parameters may be defined via the parameter
    [route_parameters](#route_parameters)
-   The result must be a json array with the results in the format:
    `[{ code: id; label: "Label" }]`

```yaml
filter:
    myFilter:
        route: my_entity_autocomplete_route
```

### route_parameters

**type**: `array`

Optional additional parameters for the route defined in [route](#route).
Default is an empty array.

```yaml
filter:
    myFilter:
        route: my_entity_autocomplete_route
        route_parameters: { foo: "bar" }
```

### minimum_input_length

**type**: `int`

The minimum number of characters before an autocomplete search is
started. Default is [3]{.title-ref}.

```yaml
filter:
    myFilter:
        minimum_input_length: 5
```

### initial_value

**type**: `string|null`

If set, this filter will be initially have a set value and the list will
initially be filtered by this value. This must be a method of the
repository defined by the parameter
[initial_value_repository](#initial_value_repository) which returns
either a single object or an array with at least one entry (the first
entry will be used). Default [null]{.title-ref}.

```yaml
columns:
    myFilter:
        initial_value: findByFoo
        initial_value_repository: AppBundle\Repository\MyEntityRepository
```

### initial_value_arguments

**type**: [array\|null]{.title-ref}

Optional arguments that will be added to the call of the repository
method in parameter [initial_value](#initial_value). Default is
[null]{.title-ref}.

```yaml
columns:
    myFilter:
        initial_value: findByFoo
        initial_value_arguments: { foo: 'bar' }
```

### initial_value_repository

**type**: `string|null`

This parameter is needed and no longer optional if
[initial_value](#initial_value) is not null.

Either the name of a public service that points to the entity\'s
repository or the FQCN of the entity to be used on
EntityManager::getRepository(). This will be used to find the initial
value.

Default is [null]{.title-ref}.

```yaml
columns:
    myFilter:
        initial_value: findByFoo
        initial_value_repository: AppBundle\Repository\MyEntityRepository
```

### initial_value_choice_label

**type**: `string|null`

Property of the entity that will be used as label of the initial value
if [initial_value](#initial_value) is set. Default is
[null]{.title-ref}.

```yaml
filter:
    myFilter:
        initial_value: findByFoo
        initial_value_repository: AppBundle\Repository\MyEntityRepository
        initial_value_choice_label: title
```
