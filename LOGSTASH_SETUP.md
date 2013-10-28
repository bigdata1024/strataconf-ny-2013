### LogStash Setup ####

Create the following folders

```shell
mkdir -p /usr/local/logstash/conf /usr/local/logstash/logs

```

### Copy Your Logstash Binary To /usr/local/logstash ###

```
mv ~/Downloads/logstash-1.2.2-flatjar.jar /usr/local/logstash/

```

Create the following Configuration File for Logstash


```

vi /usr/local/logstash/conf/stata.demo.conf


```


```
input {

    file {
      type => "CATALINA"

      path => "/usr/local/tomcat7/logs/catalina.log"

      start_position => "beginning"

    }


    file {
      type => "ACCESS"
      path => "/usr/local/tomcat7/logs/localhost_access_log*"
      start_position => "beginning"
    }
}


output {

  elasticsearch_http {
    flush_size => 256
    idle_flush_time => 2
    host => "127.0.0.1"
    port => 9200
  }
}

```
