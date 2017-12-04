[![Build Status](https://travis-ci.org/mozilla/moztelemetry.svg?branch=master)](https://travis-ci.org/mozilla/moztelemetry)
[![codecov.io](https://codecov.io/github/mozilla/moztelemetry/coverage.svg?branch=master)](https://codecov.io/github/mozilla/moztelemetry?branch=master)
[![CircleCi](https://circleci.com/gh/mozilla/moztelemetry.svg?style=shield&circle-token=3fff2168f7d8da61b47bd1481c4fcb984ec88ef5)](https://circleci.com/gh/mozilla/moztelemetry)

# moztelemetry

Mozilla's Telemetry API for Scala

## Using moztelemetry

In SBT:
```
resolvers += "S3 local maven snapshots" at "s3://net-mozaws-data-us-west-2-ops-mavenrepo/snapshots"
libraryDependencies += "com.mozilla.telemetry" %% "moztelemetry" % "1.0-SNAPSHOT"
```

## Testing

To run the tests, build the docker container and run the tests.

Build the container. You only have to do this once or when you update the Dockerfile:

```
docker build -t moztelemetry .
```

Run the tests in the docker container:

```
./bin/test
```

Other test tasks can by run by passing the task through the test script, e.g.:

```
./bin/test "testOnly com.mozilla.telemetry.stats.StatsTest"
```

## Publishing snapshots

Snapshots will now be published to our local maven repo in s3 on every commit merged into master via a circleci build

## Inspecting the Generated Protoc Case Classes

We use protoc to generate case classes which decode (and encode) the protobuf byte arrays.

You can inspect the functions in the generated Field class:
```
sbt compile
cd target/scala-2.11/classes/com/mozilla/telemetry/heka/
javap -c Field\$.class
```

There are more components of the field class, which can be seen by simply running `ls`. For example:
```
Field$ValueTypeEnum$.class
Field$ValueTypeEnum$BOOL$.class
Field$ValueTypeEnum$BYTES$.class
Field$ValueTypeEnum$DOUBLE$.class
Field$ValueTypeEnum$INTEGER$.class
Field$ValueTypeEnum$STRING$.class
Field$ValueTypeEnum$Unrecognized$.class
Field$ValueTypeEnum$Unrecognized.class
Field$ValueTypeEnum$class.class
Field$ValueTypeEnum.class
```
