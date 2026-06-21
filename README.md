# ISP-Lab-BGP-OSPF-CGNAT
LAB ISP COMPLETO – BGP + OSPF + CGNAT + DMZ + MK-AUTH


## 📡 Visão Geral

Este laboratório simula a infraestrutura de um provedor de internet (ISP), contemplando:

* Multihoming com dois provedores upstream
* BGP entre borda e operadoras
* OSPF interno
* CGNAT
* DMZ
* MK-AUTH
* Segmentação de serviços
* Loopbacks para identificação dos roteadores

---

# Topologia

```text

             ISP-A
        10.255.255.1
              |
      100.64.254.1/30
              |
      100.64.254.2/30
           BORDA
     Lo:100.255.255.3
              |
-----------------------------------------
|                   |                   |
|                   |                   |
CGNAT             DMZ            CONCENTRADOR
2.0.0.1          2.0.0.2            2.0.0.0
```

---

# Operadoras

## ISP-A

Loopback:

```text
10.255.255.1
```

Link com Borda:

```text
ISP-A  -> 100.64.254.1/30
BORDA  -> 100.64.254.2/30
```

---

## ISP-B

Loopback:

```text
10.255.255.2
```

Link com Borda:

```text
ISP-B  -> 100.90.0.1/30
BORDA  -> 100.90.0.2/30
```

---

# Borda

Loopback:

```text
100.255.255.3
```

Links para os concentradores:

```text
BORDA 100.90.0.5  <-> 100.90.0.6 CONCENTRADOR

BORDA 100.90.0.9  <-> 100.90.0.10 CONCENTRADOR
```

Link adicional:

```text
BORDA 100.64.254.17/30
CONCENTRADOR 100.64.254.18/30
```

---

# Concentrador

Rede anunciada:

```text
2.0.0.0/24
```

Responsável por:

* PPPoE
* Distribuição dos assinantes
* Encaminhamento para CGNAT
* Integração com MK-AUTH

---

# CGNAT

Loopback:

```text
2.0.0.1
```

Link com Borda:

```text
BORDA 100.64.254.21/30
CGNAT 100.64.254.22/30
```

Link com Concentrador:

```text
CONCENTRADOR 100.64.254.29/30
CGNAT       100.64.254.30/30
```

---

# DMZ

Loopback:

```text
2.0.0.2
```

Link com Borda:

```text
BORDA 100.64.254.25/30
DMZ   100.64.254.26/30
```

---

# Estrutura CGNAT

## Quantidade de portas

Cada endereço IPv4 possui:

```text
65.512 portas disponíveis
```

Divisão adotada:

```text
2.016 portas por cliente
```

Capacidade:

```text
32 clientes por IP público
```

Pool Público:

```text
8 IPs públicos
```

Capacidade Total:

```text
256 clientes
```

---

## Faixa Privada dos Assinantes

```text
100.64.0.0/24
```

---

## Pool Público CGNAT

```text
Rede:      2.0.0.64/29
Broadcast: 2.0.0.71
```

IPs disponíveis:

```text
2.0.0.65
2.0.0.66
2.0.0.67
2.0.0.68
2.0.0.69
2.0.0.70
```

---

# Servidores (DMZ)

Rede:

```text
2.0.0.8/29
```

Detalhamento:

| Função      | Endereço |
| ----------- | -------- |
| Network     | 2.0.0.8  |
| Gateway DMZ | 2.0.0.9  |
| MK-AUTH     | 2.0.0.10 |
| Broadcast   | 2.0.0.15 |

---

# Protocolos Utilizados

## BGP

Utilizado para:

* Conexão com ISP-A
* Conexão com ISP-B
* Redundância de trânsito
* Engenharia de tráfego

---

## OSPF

Utilizado internamente para:

* Troca de rotas entre roteadores
* Divulgação das Loopbacks
* Integração entre:

  * Borda
  * Concentrador
  * CGNAT
  * DMZ

---

# Objetivos do Laboratório

* Simular ambiente real de ISP
* Estudar BGP multihomed
* Implementar CGNAT
* Implementar DMZ
* Integrar MK-AUTH
* Praticar OSPF
* Aplicar boas práticas de roteamento
* Desenvolver troubleshooting de ambiente ISP

---

## Tecnologias

* Mikrotik RouterOS
* EVE-NG
* BGP
* OSPF
* NAT
* CGNAT
* PPPoE
* MK-AUTH

---

## Autor

Jhonatan Bernardino da Silva

Analista NOC | Infraestrutura de Redes | Linux | Zabbix | Grafana | Automação
