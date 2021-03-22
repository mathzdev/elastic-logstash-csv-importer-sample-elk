# A simple model to import your csv into elasticsearch using logstash

## First Step

Certify if you have logstash in your machine, or download here https://www.elastic.co/pt/downloads/logstash

## Second Step

You need to see the logstash.conf file and its structure, and adapt it if necessary. 

```
input {
  file {
    path => "cities.csv"
    start_position => "beginning"
  }
}

filter {  
  csv {
    separator => ","
    columns => ["LatD", "LatM", "LatS", "NS", "LonD", "LonM", "LonS", "EW", "City", "State"]
  }
}

output {
  elasticsearch { 
    hosts => ["localhost:9200"] 
    index => "cities"
  }
}
```

### Input
The input section is about your file and respective configurations, in this case only setting the start position for the logstash start reading. Sometimes in path need to put real path like "D:/PATH/TO/YOUR/CITIES/cities.csv".

### Filter
The filter section is about your file structure, and the separation of columns and values. And have de mutate additional parameters, to mutate your data, in this case we using strip to remove whitespaces after and before any word, and removing dumb columns ("path", "host", "message").

### Output
The output section is to set your index (the collection to save the data) and your host destiny (address to elasticsearch).

### More about config file 
See more at https://www.elastic.co/guide/en/logstash/master/configuration-file-structure.html

## Third Step
Now is ready to run the simple command ```logstash -f logstash.conf``` and the magic starts! Do you need to wait the process (maybe to take a time :D)...

### Kibana showing your data
See in kibana your data after import:

#### All data

 ![Using](https://raw.githubusercontent.com/fenxlol/elastic-logstash-csv-importer-sample-elk/main/using1.png)
 
#### And Filtering

![Using](https://raw.githubusercontent.com/fenxlol/elastic-logstash-csv-importer-sample-elk/main/using2.png)

# Enjoy the ELK stack !

## Credits
Me [@fenxlol](https://github.com/fenxlol) [Matheus's Linkedin](https://www.linkedin.com/in/matheuslucio/) to create this simple tuto, and [@WilsonLucas](https://github.com/WilsonLucas) [Wilson's Linkedin](https://www.linkedin.com/in/wilson-lucas-719963b4/) for teach me about logstash.

![Elk Stack](https://raw.githubusercontent.com/fenxlol/elastic-logstash-csv-importer-sample-elk/main/elk-stack-logo.png)