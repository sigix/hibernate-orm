# Building Patch JAR

- where `n` is the current version:
  - `git grep -l '3.6.3.Final' -- "*pom.xml" | xargs -n 1 sed -i "" "s/3.6.3.Final-appian-1.(n)/3.6.3.Final-appian-1.(n+1)/"`
- `cd hibernate-core`
- `mvn clean`
- comment out the `commons-logging` dependencies in `hibernate-parent/pom.xml`
  - search for `APPIAN`
- `mvn install -pl hibernate-core`
- uncomment `commons-logging` dependencies in `hibernate-parent/pom.xml`
- JAR is available at `hibernate-core/target/hibernate-core-3.6.3.Final-appian-1.(n+1).jar`
- Sources JAR is available at `hibernate-core/target/hibernate-core-3.6.3.Final-appian-1.(n+1)-sources.jar`

# Uploading Patch JAR to Artifactory

- upload the following objects:
  - `hibernate-core/target/hibernate-core-3.6.3-Final-appian-1.(n).jar`
    - upload single file, as a Maven artifact
  - `hibernate-core/target/hibernate-core-3.6.3-Final-appian-1.(n)-sources.jar`
    - upload single file, specify `org.hibernate` as group ID, specify `sources` as Classifier
  - `hibernate-core/pom.xml`
    - specify group / artifact IDs, specify type as `pom`
  - `hibernate-parent/pom.xml`
    - upload single file under `hibernate-parent`
    - specify as Maven artifact, use POM
    - use `org.hibernate` as group ID, `hibernate-parent` as artifact ID
    - specify `pom` as type
