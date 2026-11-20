# POL-ACESSO-001 — Política de Gestão de Identidade e Acesso

**Empresa:** Acme Serviços Financeiros S.A. (documento fictício para fins acadêmicos)
**Classificação:** Interno
**Versão:** 3.2
**Vigência:** a partir de 01/09/2026
**Dono do documento:** Diretoria de Segurança da Informação (CISO)

## 1. Objetivo
Estabelecer as regras de concessão, revisão e revogação de acessos lógicos aos sistemas da Acme, garantindo que cada identidade tenha apenas os acessos necessários à sua função.

## 2. Princípios
2.1. Menor privilégio: o padrão de qualquer acesso é o mínimo necessário para a função. Acesso amplo exige justificativa documentada.
2.2. Necessidade de conhecer: acesso a dados classificados como Confidencial ou Restrito só é concedido quando a função exige.
2.3. Acesso é sempre vinculado a um papel (role) do catálogo (ver NORMA-PERFIS-001). Acesso direto a permissão, fora de papel, só é permitido como exceção aprovada.
2.4. Toda concessão tem um dono de recurso responsável pela aprovação.

## 3. Sistemas de identidade
3.1. Entra ID: provedor de identidade corporativo e SSO.
3.2. SailPoint IdentityIQ: plataforma de governança (solicitação, aprovação, certificação).
3.3. CyberArk: cofre de acesso privilegiado (ver PROC-PAM-001).
3.4. SAP: ERP financeiro.

## 4. Ciclo de vida (joiner, mover, leaver)
4.1. Admissão (joiner): o acesso base é provisionado automaticamente pelo RH via Entra ID, por cargo. Não requer aprovação manual.
4.2. Movimentação (mover): ao mudar de área ou cargo, os acessos da função anterior são revogados em até 5 dias úteis. Acessos que o colaborador queira manter exigem nova solicitação e aprovação.
4.3. Desligamento (leaver): todos os acessos são revogados em até 4 horas após a notificação de desligamento pelo RH. Contas privilegiadas são revogadas imediatamente.

## 5. Pedidos fora do padrão (exceções)
5.1. Qualquer pedido que não seja atendido pela automação de cargo é tratado como exceção e segue por SailPoint.
5.2. Aprovadores obrigatórios de uma exceção:
   a) dono do recurso solicitado;
   b) gestor direto do solicitante;
   c) DPO, quando o acesso envolver dado pessoal classificado como Restrito (ver LGPD-CLASS-001);
   d) time de IAM, quando houver conflito de SoD (ver SOD-MATRIZ-001).
5.3. Acesso de exceção é sempre temporário: prazo máximo de 90 dias, com recertificação obrigatória para renovar. Sem recertificação no prazo, o acesso é revogado automaticamente.
5.4. É proibido um solicitante aprovar o próprio pedido de acesso, em qualquer sistema.

## 6. Segregação de funções (SoD)
6.1. Antes de conceder qualquer acesso, o time de IAM verifica conflito de SoD na SOD-MATRIZ-001.
6.2. Conflito classificado como Crítico: acesso negado. Só pode ser concedido com controle compensatório formal e aprovação do CISO e do Auditor Interno.
6.3. Conflito classificado como Alto: acesso permitido apenas com controle compensatório documentado e aprovação do gestor da área e do dono do recurso.

## 7. Revisão periódica de acessos (certificação)
7.1. Acessos privilegiados: certificação trimestral.
7.2. Acessos a dados Restritos: certificação trimestral.
7.3. Demais acessos: certificação semestral.
7.4. Acesso não confirmado na certificação é revogado em até 10 dias úteis.

## 8. Decisão padrão do assistente de governança
8.1. Quando a política for clara, o assistente responde PODE ou NÃO PODE e cita o item.
8.2. Quando o pedido exigir aprovação adicional (exceção, SoD Alto, dado Restrito, acesso privilegiado), o assistente responde PRECISA APROVAÇÃO ADICIONAL e indica quais aprovadores dos itens 5.2, 6.2, 6.3 ou do PROC-PAM-001.
8.3. Na ausência de base na política, o assistente não decide: responde que não há política aplicável e orienta abrir exceção.
