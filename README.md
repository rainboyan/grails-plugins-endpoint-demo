# Grails 2022 New Features

This is a demo build by Grails 2022.0.0

> Actuator endpoints let you monitor and interact with your application.
> Spring Boot Actuator provides the infrastructure required for actuator endpoints.

To enable Spring Boot Actuator, For Gradle, use the following declaration:

```gradle
	dependencies {
		implementation 'org.springframework.boot:spring-boot-starter-actuator'
	}
```

Now in Grails `2022.0.0`, we also add this feature:
The `plugins` endpoint provides basic Grails plugins information. 
The `info` endpoint provides basic Grails Application information. 

Run up a basic Grails application and look at `/actuator/plugins`.

### Config `application.yml`

```yml
environments:
    development:
        management:
            info:
                java:
                    enabled: true
                os:
                    enabled: true
            endpoints:
                enabled-by-default: true
                web:
                    base-path: '/actuator'
                    exposure:
                        include: '*'
    production:
        management:
            endpoints:
                enabled-by-default: false
```

### Endpoint `plugins`

```bash
➜  ~ http :8080/actuator/plugins
HTTP/1.1 200
Connection: keep-alive
Content-Type: application/vnd.spring-boot.actuator.v3+json
Date: Tue, 15 Nov 2022 05:00:13 GMT
Keep-Alive: timeout=60
Transfer-Encoding: chunked
Vary: Origin
Vary: Access-Control-Request-Method
Vary: Access-Control-Request-Headers

{
    "plugins": [
        {
            "dependencies": [],
            "name": "eventBus",
            "type": "org.grails.plugins.events.EventBusGrailsPlugin",
            "version": "5.0.0-SNAPSHOT"
        },
        {
            "dependencies": [],
            "name": "i18n",
            "type": "org.grails.plugins.i18n.I18nGrailsPlugin",
            "version": "2022.0.0-SNAPSHOT"
        },
        {
            "dependencies": [],
            "name": "restResponder",
            "type": "org.grails.plugins.web.rest.plugin.RestResponderGrailsPlugin",
            "version": "2022.0.0-SNAPSHOT"
        },
        {
            "dependencies": [],
            "name": "core",
            "type": "org.grails.plugins.core.CoreGrailsPlugin",
            "version": "2022.0.0-SNAPSHOT"
        },
        {
            "dependencies": [
                "core",
                "i18n",
                "urlMappings"
            ],
            "name": "controllers",
            "type": "org.grails.plugins.web.controllers.ControllersGrailsPlugin",
            "version": "2022.0.0-SNAPSHOT"
        },
        {
            "dependencies": [
                "core"
            ],
            "name": "urlMappings",
            "type": "org.grails.plugins.web.mapping.UrlMappingsGrailsPlugin",
            "version": "2022.0.0-SNAPSHOT"
        },
        {
            "dependencies": [
                "i18n"
            ],
            "name": "domainClass",
            "type": "org.grails.plugins.domain.DomainClassGrailsPlugin",
            "version": "2022.0.0-SNAPSHOT"
        },
        {
            "dependencies": [],
            "name": "fields",
            "type": "grails.plugin.formfields.FieldsGrailsPlugin",
            "version": "5.0.0-SNAPSHOT"
        },
        {
            "dependencies": [
                "core",
                "i18n"
            ],
            "name": "groovyPages",
            "type": "org.grails.plugins.web.GroovyPagesGrailsPlugin",
            "version": "5.2.2-SNAPSHOT"
        },
        {
            "dependencies": [
                "core"
            ],
            "name": "codecs",
            "type": "org.grails.plugins.codecs.CodecsGrailsPlugin",
            "version": "2022.0.0-SNAPSHOT"
        },
        {
            "dependencies": [],
            "name": "scaffolding",
            "type": "grails.plugin.scaffolding.ScaffoldingGrailsPlugin",
            "version": "5.0.0-SNAPSHOT"
        },
        {
            "dependencies": [
                "controllers"
            ],
            "name": "converters",
            "type": "org.grails.plugins.converters.ConvertersGrailsPlugin",
            "version": "2022.0.0-SNAPSHOT"
        },
        {
            "dependencies": [],
            "name": "hibernate",
            "type": "grails.plugin.hibernate.HibernateGrailsPlugin",
            "version": "7.2.3-SNAPSHOT"
        },
        {
            "dependencies": [],
            "name": "assetPipeline",
            "type": "asset.pipeline.AssetPipelineGrailsPlugin",
            "version": "3.4.6"
        },
        {
            "dependencies": [],
            "name": "controllersAsync",
            "type": "org.grails.plugins.web.async.ControllersAsyncGrailsPlugin",
            "version": "5.0.0-SNAPSHOT"
        },
        {
            "dependencies": [
                "controllers",
                "urlMappings"
            ],
            "name": "interceptors",
            "type": "org.grails.plugins.web.interceptors.InterceptorsGrailsPlugin",
            "version": "2022.0.0-SNAPSHOT"
        },
        {
            "dependencies": [],
            "name": "services",
            "type": "org.grails.plugins.services.ServicesGrailsPlugin",
            "version": "2022.0.0-SNAPSHOT"
        },
        {
            "dependencies": [],
            "name": "cache",
            "type": "grails.plugin.cache.CacheGrailsPlugin",
            "version": "5.0.1"
        }
    ]
}
```

### Endpoint `info`

```bash
curl 'http://localhost:8080/actuator/info' | fx
```

```bash
➜  ~ http :8080/actuator/info
HTTP/1.1 200
Connection: keep-alive
Content-Type: application/vnd.spring-boot.actuator.v3+json
Date: Tue, 15 Nov 2022 04:59:39 GMT
Keep-Alive: timeout=60
Transfer-Encoding: chunked
Vary: Origin
Vary: Access-Control-Request-Method
Vary: Access-Control-Request-Headers

{
    "app": {
        "grailsVersion": "2022.0.0-SNAPSHOT",
        "name": "grails-plugins-endpoint-demo",
        "version": "0.1"
    },
    "java": {
        "jvm": {
            "name": "OpenJDK 64-Bit Server VM",
            "vendor": "Azul Systems, Inc.",
            "version": "11.0.15+10-LTS"
        },
        "runtime": {
            "name": "OpenJDK Runtime Environment",
            "version": "11.0.15+10-LTS"
        },
        "vendor": {
            "name": "Azul Systems, Inc.",
            "version": "Zulu11.56+19-CA"
        },
        "version": "11.0.15"
    },
    "os": {
        "arch": "aarch64",
        "name": "Mac OS X",
        "version": "12.6.1"
    }
}
```