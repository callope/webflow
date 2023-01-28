# WebFlow

A minimalist package to help you build powerful asynchronous
web-hooks.

## Installation

This package is available on PyPi, so you can install it with
`pip install webflow`.

## Usage

```
from flask import Flask
from flow import Flow
from somewhere import detect_event

app = Flask(__name__)
flow = Flow(app) # create flow instance passing underlying flask appplication

@flow.event(detect_event)
def callback():
  """Will be executed by Flow automatically when
  detect_event awaits True."""
  ...
```

If you want the events to be setted up in another file, do this:

```
from flask import Flask
from .webhhook import setup


app = Flask(__name__)
setup(app)
```

On `webhook.py`:

```
from flow import Flow


def setup(application):
  events = [...] # collection of tuples with (detect_function, callback)

  flow = Flow(application)
  for df, callback in events:
    flow.new(df, callback)
```
