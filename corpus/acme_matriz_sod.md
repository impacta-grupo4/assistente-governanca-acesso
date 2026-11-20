# SOD-MATRIZ-001 — Matriz de Segregação de Funções (SoD)

**Empresa:** Acme Serviços Financeiros S.A. (documento fictício para fins acadêmicos)
**Classificação:** Confidencial
**Versão:** 2.5
**Vigência:** a partir de 01/09/2026
**Dono do documento:** Auditoria Interna, com apoio do time de IAM

## 1. Objetivo
Listar as combinações de funções que não podem coexistir na mesma identidade, por gerarem risco de fraude ou erro sem detecção. Esta matriz é a fonte citada pelo assistente em qualquer análise de conflito.

## 2. Classificação dos conflitos
- **Crítico:** risco direto de fraude financeira. Acesso negado por padrão. Exceção exige controle compensatório e aprovação do CISO e da Auditoria Interna (POL-ACESSO-001, item 6.2).
- **Alto:** risco relevante de erro ou abuso. Acesso permitido só com controle compensatório e aprovação do gestor e do dono do recurso (POL-ACESSO-001, item 6.3).
- **Médio:** monitorar. Acesso permitido, com alerta na certificação trimestral.

## 3. Matriz de conflitos

### 3.1. Conflitos Críticos
| ID | Função A | Função B | Risco |
|----|----------|----------|-------|
| SOD-C1 | Cadastro de Fornecedor (SAP) | Aprovação de Pagamento (SAP) | Criar fornecedor fantasma e pagar a ele |
| SOD-C2 | Lançamento de Contas a Pagar (SAP) | Conciliação Bancária (SAP) | Lançar pagamento e esconder na conciliação |
| SOD-C3 | Administrador de Identidade (SailPoint/Entra ID) | Auditor dos logs de identidade | Conceder acesso e apagar o próprio rastro |
| SOD-C4 | Solicitante de Acesso | Aprovador do mesmo pedido | Autoaprovação de privilégio |

### 3.2. Conflitos Altos
| ID | Função A | Função B | Risco |
|----|----------|----------|-------|
| SOD-A1 | Desenvolvedor (código) | Deploy em Produção | Subir código não revisado para produção |
| SOD-A2 | Administrador de Infraestrutura | Gestão de Backup e Restore | Apagar dado e também o backup |
| SOD-A3 | Contas a Pagar (lançamento) | Cadastro de Fornecedor (SAP) | Direcionar pagamento a dado que ele mesmo criou |
| SOD-A4 | Aprovador de Pagamento | Gestão de Limites de Alçada | Elevar o próprio limite e aprovar |

### 3.3. Conflitos Médios
| ID | Função A | Função B | Risco |
|----|----------|----------|-------|
| SOD-M1 | Suporte N1 (reset de senha) | Aprovação de Acesso | Reset indevido combinado com concessão |
| SOD-M2 | Gestor de Área | Certificador dos acessos da própria área | Confirmar acesso sem análise crítica |

## 4. Regra de leitura para o assistente
4.1. Se o pedido junta duas funções da seção 3.1, a resposta é NÃO PODE (conflito Crítico) e cita o ID SOD-C correspondente.
4.2. Se junta duas funções da seção 3.2, a resposta é PRECISA APROVAÇÃO ADICIONAL (conflito Alto, gestor e dono do recurso) e cita o ID SOD-A.
4.3. Se junta duas funções da seção 3.3, a resposta é PODE com observação de monitoramento, e cita o ID SOD-M.
4.4. Se as funções não estão na matriz, não há conflito de SoD registrado: o assistente segue a análise normal da POL-ACESSO-001.
