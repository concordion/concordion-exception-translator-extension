[![Build Status](https://travis-ci.org/concordion/concordion-exception-translator-extension.svg?branch=master)](https://travis-ci.org/concordion/concordion-exception-translator-extension)

This [Concordion](http://www.concordion.org) extension provides the capability to modify exception message text. While initially created to remove superfluous debug information from WebDriver exception messages, it could be used for translating exception messages to other languages.

The [demo project](http://github.com/concordion//concordion-exception-translator-extension-demo) demonstrates this extension using Concordion with Selenium WebDriver.

# Installation
The extension is available from [Maven Central](http://search.maven.org/#artifactdetails%7Corg.concordion%7Cconcordion-exception-translator-extension%7C1.1.2%7Cjar).</a>

# Introduction

The easiest way to configure is to use the `@Extension` annotation on an instance field of type `ExceptionTranslatorExtension` within the fixture class. 

For example, the following code configures the extension to remove text from the exception message starting from the string "Debug info:".

```java
        @Extension
        public ConcordionExtension extension =
            new ExceptionTranslatorExtension(new ExampleMessageTranslator());
```

where `ExampleMessageTranslator` is:

```java
        public class ExampleMessageTranslator() implements MessageTranslator {

            @Override
            public String translate(String originalMessage) {
                int debugInfoStart = originalMessage.indexOf("Build info:");
                if (debugInfoStart > 0) {
                    return originalMessage.substring(0, debugInfoStart);
                }
                return originalMessage;
            }
        }
```

# Further info

* [Specification](http://concordion.github.io/concordion-exception-translator-extension/spec/ExceptionTranslator.html)
* [API](http://concordion.github.io/concordion-exception-translator-extension/api/index.html)
* [Demo project](http://github.com/concordion/concordion-exception-translator-extension-demo)