# PyLoggy

`PyLoggy` is a versatile and easy-to-use Python logging utility that facilitates setting up and managing logging handlers for both console and file outputs. It supports customizable formats and logging levels, making it a powerful tool for any Python project.

## Features

- Log messages to both console and file
- Customizable log formats
- Dynamic logging level updates
- Support for multiple logging handlers

## Installation

Clone the repository from GitHub:

```
git clone https://github.com/your-username/pyloggy.git
```

## Usage

Here's how to use `PyLoggy`:

```python
import logging
import sys

class PyLoggy:
    def __init__(self, log_file=None, level=logging.DEBUG, format_str=None):
        self.logger = logging.getLogger('PyLoggy')
        self.logger.setLevel(level)
        self.handlers = []
        self.add_handler(logging.StreamHandler(sys.stdout), level, format_str)
        if log_file:
            self.add_handler(logging.FileHandler(log_file), level, format_str)
    
    def add_handler(self, handler, level=logging.DEBUG, format_str=None):
        """Add a logging handler."""
        handler.setLevel(level)
        formatter = logging.Formatter(format_str or '%(asctime)s - %(name)s - %(levelname)s - %(message)s')
        handler.setFormatter(formatter)
        self.logger.addHandler(handler)
        self.handlers.append(handler)
    
    def update_level(self, level):
        """Update the logging level for all handlers."""
        self.logger.setLevel(level)
        for handler in self.handlers:
            handler.setLevel(level)
    
    def debug(self, message):
        self.logger.debug(message)
    
    def info(self, message):
        self.logger.info(message)
    
    def warning(self, message):
        self.logger.warning(message)
    
    def error(self, message):
        self.logger.error(message)
    
    def critical(self, message):
        self.logger.critical(message)

# Example usage:
if __name__ == "__main__":
    logger = PyLoggy(log_file="example.log", format_str='%(asctime)s - %(levelname)s - %(message)s')
    logger.debug("This is a debug message")
    logger.info("This is an info message")
    logger.warning("This is a warning message")
    logger.error("This is an error message")
    logger.critical("This is a critical message")
    logger.add_handler(logging.StreamHandler(sys.stderr), level=logging.WARNING, format_str='%(asctime)s - %(levelname)s - %(message)s')
    logger.warning("This is a warning message (stderr)")
    logger.error("This is an error message (stderr)")
```

## API Reference

### `PyLoggy(log_file=None, level=logging.DEBUG, format_str=None)`

- `log_file`: Optional. Specifies the file to which logs will be written.
- `level`: Optional. Sets the initial logging level. Default is `logging.DEBUG`.
- `format_str`: Optional. Custom format string for log messages.

### Methods

- `add_handler(handler, level=logging.DEBUG, format_str=None)`: Adds a logging handler with an optional level and format string.
- `update_level(level)`: Updates the logging level for all handlers.
- `debug(message)`: Logs a debug message.
- `info(message)`: Logs an informational message.
- `warning(message)`: Logs a warning message.
- `error(message)`: Logs an error message.
- `critical(message)`: Logs a critical message.

## Example

```python
# Initialize the logger
logger = PyLoggy(log_file="example.log", format_str='%(asctime)s - %(levelname)s - %(message)s')

# Log messages of various levels
logger.debug("This is a debug message")
logger.info("This is an info message")
logger.warning("This is a warning message")
logger.error("This is an error message")
logger.critical("This is a critical message")

# Add another handler for stderr with a higher logging level
logger.add_handler(logging.StreamHandler(sys.stderr), level=logging.WARNING, format_str='%(asctime)s - %(levelname)s - %(message)s')
logger.warning("This is a warning message (stderr)")
logger.error("This is an error message (stderr)")
```

## Contact

For questions or feedback, please reach out to www.linkedin.com/in/sriram-amalakanti.
