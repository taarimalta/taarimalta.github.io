Title: Janch
Date: 2023-02-23 22:01
Category: JanchTech


Do you find it difficult to keep track of all the potential issues that could affect your software product? It's easy to get overwhelmed by the sheer number of things that could go wrong, from web service outages to low disk space and excessive error logging.

Janch is a powerful yet lightweight tool that can help you monitor your software product and ensure that everything is running smoothly. With just a few entries in a YAML file, you can set up your targets and let the tool do the rest. It reads and interprets the YAML file, giving you a clear and concise status report on all your targets.

# Example YAML config

    #!yml
    command-example:
      gather:
        type: command
        command_str: python --version
      inspect:
        result: ^Python 3\.(.*)$
    
    grep-example:
      gather:
        type: grep
        filepath: test.env
        search: '='
      inspect:
        result: (.*)=(.*)
        line_count: 1
    
    webservice-example:
      gather:
        type: http
        url: http://www.example.com
      inspect:
        status: 200

# Example Output

    item                            type    field           expected                        actual                          match error
    grep-example                    grep    result          (.*)=(.*)                       Hello=world                     True  False
    grep-example                    grep    line_count      1                               1                               True  False
    grep-example                    grep    error           NOERROR                         NOERROR                         True  False
    command-example                 command result          ^Python 3\.(.*)$                Python 3.8.2                    True  False
    command-example                 command error           NOERROR                         NOERROR                         True  False
    webservice-example              http    status          200                             200                             True  False
    webservice-example              http    error           NOERROR                         NOERROR                         True  False


# Try it

[Visit the Github Page](https://github.com/janch-tech/janch)