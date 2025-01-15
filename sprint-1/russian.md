Инструкция по запуску консьюмера и продьюсера в readme. 

Для упрощенной проверки можно использовать Kafka-UI по адресу localhost:20080.

Важно: неправильная схема данных приводит к остановке работы консьюмера. Это ожидаемое поведение, поскольку события как правило терять нельзя.  

Комменты:
- At least once - acks=1. 
- Для push модели выставляем poll=100, считываем сразу. "fetch.min.bytes" устанавливать не стал, поскольку кафка-модели небольшие
- За параллельное считывание отвечает консьюмер группа, поэтому передаю разные в makefile

Прмиер команд:
kafka-topics --bootstrap-server kafka-0:9092 --list

kafka-topics --create --if-not-exists --topic mp-messages-stream --bootstrap-server kafka-0:9092 --partitions 3 --replication-factor 2
kafka-topics --create --if-not-exists --topic mp-blocked-users-stream --bootstrap-server kafka-0:9092 --partitions 3 --replication-factor 2
kafka-topics --create --if-not-exists --topic mp-filtered-messages-stream --bootstrap-server kafka-0:9092 --partitions 3 --replication-factor 2

kafka-topics --create --if-not-exists --topic block-users-consumer-table --bootstrap-server kafka-0:9092 --partitions 3 --replication-factor 2 --config cleanup.policy=compact
