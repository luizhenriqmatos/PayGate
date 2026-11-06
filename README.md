# PayGate

PayGate — API de Processamento de Pagamentos de Alta Disponibilidade

O PayGate é um microsserviço de pagamentos que construí para resolver os problemas que mais importam quando dinheiro está em jogo: não cobrar duas vezes, não perder transações e continuar funcionando quando um sistema externo falha.

Feito em Java 21 e Spring Boot com arquitetura hexagonal. As regras de negócio ficam isoladas da infraestrutura. Cada pagamento passa por autorização e liquidação de forma assíncrona via Apache Kafka, com idempotência tanto na API quanto nos consumidores. Se o banco cai, o circuit breaker do Resilience4j isola a falha, os pagamentos ficam aguardando e são concluídos automaticamente quando o banco volta. Num teste com 580 transações e o banco fora do ar no meio do caminho, todas foram liquidadas, sem perdas nem duplicidades.

Cada pagamento pode ser rastreado de ponta a ponta por um TraceID no Grafana e no Zipkin, com métricas no Prometheus. A qualidade é garantida por 115 testes automatizados, incluindo integração com PostgreSQL e Kafka reais via Testcontainers, com 97% de cobertura de código.

O banco é simulado; o próximo passo é integrar um provedor Pix real em ambiente de sandbox.

🔗 https://paygate-luiz.netlify.app
