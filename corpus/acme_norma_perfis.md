# NORMA-PERFIS-001 — Catálogo e Norma de Perfis de Acesso

**Empresa:** Acme Serviços Financeiros S.A. (documento fictício para fins acadêmicos)
**Classificação:** Interno
**Versão:** 4.1
**Vigência:** a partir de 01/09/2026
**Dono do documento:** Time de IAM

## 1. Objetivo
Definir os perfis (roles) padrão da Acme, o que cada um concede, quem é o dono do recurso e se o perfil é privilegiado. Acesso só é concedido por meio de um perfil deste catálogo, salvo exceção aprovada (POL-ACESSO-001, item 5).

## 2. Estrutura de um perfil
Cada perfil tem: nome, sistema, permissões, dono do recurso, classificação do dado acessado (ver LGPD-CLASS-001) e marcação de privilegiado (sim/não).

## 3. Catálogo de perfis

### 3.1. Perfis de negócio
| Perfil | Sistema | Concede | Dono do recurso | Dado | Privilegiado |
|--------|---------|---------|-----------------|------|--------------|
| P-FIN-AP | SAP | Lançar contas a pagar | Gerente Financeiro | Confidencial | Não |
| P-FIN-APROV | SAP | Aprovar pagamento dentro da alçada | Diretor Financeiro | Confidencial | Não |
| P-FIN-FORN | SAP | Cadastrar e alterar fornecedor | Gerente Financeiro | Confidencial | Não |
| P-FIN-CONC | SAP | Conciliação bancária | Gerente Financeiro | Confidencial | Não |
| P-RH-FOLHA | SAP | Consultar folha de pagamento | Gerente de RH | Restrito | Não |
| P-ATEND-CLI | Okta/CRM | Consultar cadastro de cliente | Gerente de Atendimento | Restrito | Não |

### 3.2. Perfis de TI e identidade
| Perfil | Sistema | Concede | Dono do recurso | Dado | Privilegiado |
|--------|---------|---------|-----------------|------|--------------|
| P-SUP-N1 | Entra ID | Reset de senha, desbloqueio de conta | Coordenador de Suporte | Interno | Não |
| P-IAM-ADM | SailPoint/Entra ID | Criar, alterar e remover acesso de qualquer usuário | Coordenador de IAM | Restrito | Sim |
| P-INFRA-ADM | Servidores/Cloud | Administração de servidores e infraestrutura | Coordenador de Infra | Confidencial | Sim |
| P-DBA | Banco de dados | Administração de banco | Coordenador de Dados | Restrito | Sim |
| P-DEV | Repositório | Desenvolver e versionar código | Coordenador de Engenharia | Interno | Não |
| P-DEPLOY-PROD | Pipeline CI/CD | Publicar em produção | Coordenador de Engenharia | Confidencial | Sim |

### 3.3. Perfis de controle
| Perfil | Sistema | Concede | Dono do recurso | Dado | Privilegiado |
|--------|---------|---------|-----------------|------|--------------|
| P-AUD-LOG | SIEM/SailPoint | Ler logs e trilhas de acesso (somente leitura) | Auditoria Interna | Restrito | Não |
| P-DPO | Registro LGPD | Aprovar acesso a dado pessoal Restrito | DPO | Restrito | Não |

## 4. Regras de concessão por perfil
4.1. Perfis marcados como Privilegiado (coluna "Privilegiado = Sim") nunca são acesso permanente (standing). Só são usados via CyberArk, por sessão temporária (ver PROC-PAM-001).
4.2. Perfil que acessa dado Restrito exige aprovação do DPO além do fluxo normal (POL-ACESSO-001, item 5.2.c).
4.3. Acúmulo de perfis é verificado contra a SOD-MATRIZ-001 antes da concessão.
4.4. Suporte N1 (P-SUP-N1) não concede nenhum acesso administrativo. Reset de senha não é acesso privilegiado.

## 5. Regra de leitura para o assistente
5.1. Para saber se um acesso é privilegiado, o assistente consulta a coluna "Privilegiado" deste catálogo, não o nome do cargo.
5.2. Pedido de perfil privilegiado como acesso permanente: resposta NÃO PODE, e redireciona para PROC-PAM-001 (sessão temporária).
5.3. Pedido de perfil que acessa dado Restrito: resposta PRECISA APROVAÇÃO ADICIONAL (DPO).
