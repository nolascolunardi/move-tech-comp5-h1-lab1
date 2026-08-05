# ADR 001 — Usar K3s em VM para orquestração da aplicação

**Status:** Aceito  
**Data:** 2026-08-04

## Contexto
A aplicação precisa de uma plataforma de orquestração para executar a API,
gerenciar deployments, escalabilidade, atualizações e integração com os demais
serviços da infraestrutura. O ambiente é de pequeno porte e não exige um
cluster Kubernetes gerenciado.

## Alternativas consideradas
- **K3s em VM** — distribuição Kubernetes leve, baixo consumo de recursos,
  compatível com o ecossistema Kubernetes; exige administração da VM e do
  cluster.
- **MKS (Magalu Kubernetes Service)** — Kubernetes gerenciado pelo provedor,
  menor esforço operacional; maior custo e dependência dos recursos oferecidos
  pelo serviço.
- **VM com Docker Compose** — simples de configurar e operar; adequado para
  aplicações pequenas, porém sem recursos nativos de orquestração, alta
  disponibilidade e escalabilidade.

## Decisão
Utilizar **K3s em uma VM** para hospedar a aplicação. O critério decisivo foi
equilibrar baixo custo com a necessidade de utilizar Kubernetes, mantendo
compatibilidade com ferramentas do ecossistema e permitindo evoluir a
infraestrutura sem depender de um serviço gerenciado.

## Consequências

**Positivas:**
- Compatibilidade com o ecossistema Kubernetes.
- Baixo consumo de recursos em comparação ao Kubernetes tradicional.
- Menor custo em relação a um cluster gerenciado (MKS).
- Permite utilizar Deployments, Services, Ingress, Secrets e ConfigMaps.
- Facilidade para evoluir a infraestrutura futuramente.

**Negativas:**
- Administração da VM e do cluster é responsabilidade da equipe.
- Atualizações e manutenção do K3s precisam ser realizadas manualmente.
- Não possui alta disponibilidade nativa em uma única VM.
- Exige monitoramento e backups da infraestrutura.
