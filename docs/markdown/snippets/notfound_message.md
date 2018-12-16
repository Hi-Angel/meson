## New `notfound_message` for dependency

You can now specify a `notfound_message` that will be printed if the
specified dependency was not found. The point is to convert constructs
that look like this:

```meson
d = dependency('something', required: false)
if not d.found()
  message('Will not be able to do something.')
endif
```

Into this:

```meson
d = dependency('something',
  required: false,
  notfound_message: 'Will not be able to do something.')
```

Or constructs like this:

```meson
d = dependency('something', required: false)
if not d.found()
  error('Install something by doing XYZ.')
endif
```

into this:

```meson
d = dependency('something',
  notfound_message: 'Install something by doing XYZ.')
```

Which works, because the default value of `required` is `true`.
