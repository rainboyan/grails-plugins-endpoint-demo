# Grails 2022 New Feature: Plugins Endpoint Demo

This is a demo build by Grails 2022.0.0

> Actuator endpoints let you monitor and interact with your application.
> Spring Boot Actuator provides the infrastructure required for actuator endpoints.

To enable Spring Boot Actuator, For Gradle, use the following declaration:

[indent=0]
----
	dependencies {
		implementation 'org.springframework.boot:spring-boot-starter-actuator'
	}
----

Now in Grails `2022.0.0`, we also add this feature:
The `plugins` endpoint provides basic Grails plugins information. Run up a basic Grails application and look at `/actuator/plugins`.

```bash
curl 'http://localhost:8080/actuator/plugins' | fx
```

The resule:

```json
{
  "plugins": [
    {
      "name": "restResponder",
      "type": "org.grails.plugins.web.rest.plugin.RestResponderGrailsPlugin",
      "version": "2022.0.0-SNAPSHOT",
      "dependencies": []
    },
    {
      "name": "i18n",
      "type": "org.grails.plugins.i18n.I18nGrailsPlugin",
      "version": "2022.0.0-SNAPSHOT",
      "dependencies": []
    },
    {
      "name": "eventBus",
      "type": "org.grails.plugins.events.EventBusGrailsPlugin",
      "version": "5.0.0-SNAPSHOT",
      "dependencies": []
    },
    {
      "name": "core",
      "type": "org.grails.plugins.core.CoreGrailsPlugin",
      "version": "2022.0.0-SNAPSHOT",
      "dependencies": []
    },
    {
      "name": "codecs",
      "type": "org.grails.plugins.codecs.CodecsGrailsPlugin",
      "version": "2022.0.0-SNAPSHOT",
      "dependencies": [
        "core"
      ]
    },
    {
      "name": "controllers",
      "type": "org.grails.plugins.web.controllers.ControllersGrailsPlugin",
      "version": "2022.0.0-SNAPSHOT",
      "dependencies": [
        "core",
        "i18n",
        "urlMappings"
      ]
    },
...
}
```