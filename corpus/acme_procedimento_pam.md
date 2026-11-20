# PROC-PAM-001 — Procedimento de Acesso Privilegiado

**Empresa:** Acme Serviços Financeiros S.A. (documento fictício para fins acadêmicos)
**Classificação:** Confidencial
**Versão:** 2.0
**Vigência:** a partir de 01/09/2026
**Dono do documento:** Time de IAM, com apoio da Segurança da Informação

## 1. Objetivo
Definir como o acesso privilegiado (administrativo) é solicitado, concedido e usado na Acme. Aplica-se a todos os perfis marcados como Privilegiado = Sim na NORMA-PERFIS-001.

## 2. Princípios do acesso privilegiado
2.1. Nenhum acesso administrativo é permanente. Todo uso é temporário e justificado (just-in-time).
2.2. Todo acesso privilegiado passa pelo cofre CyberArk. Não existe conta administrativa fora do cofre.
2.3. Conta privilegiada é individual. É proibido compartilhar conta administrativa.
2.4. MFA resistente a phishing (FIDO2 ou certificado) é obrigatório para qualquer sessão privilegiada. Código por SMS não é aceito.

## 3. Solicitação de sessão privilegiada
3.1. A sessão é solicitada no CyberArk, com justificativa e janela de tempo.
3.2. Duração máxima de uma sessão privilegiada: 8 horas. Após isso, a sessão encerra e exige nova solicitação.
3.3. Aprovadores de uma sessão privilegiada:
   a) dono do recurso (coluna "Dono do recurso" da NORMA-PERFIS-001);
   b) gestor direto do solicitante.
3.4. Toda sessão privilegiada é gravada e os logs vão para o SIEM, com retenção mínima de 12 meses.

## 4. Acesso de emergência (break-glass)
4.1. Usado apenas em incidente, quando o fluxo normal não pode ser seguido a tempo.
4.2. Exige aprovação de 2 pessoas distintas (dupla custódia), uma delas da Segurança da Informação.
4.3. Janela máxima de 4 horas.
4.4. Revisão obrigatória em até 24 horas após o uso, pela Auditoria Interna. Uso sem revisão no prazo é tratado como incidente de segurança.

## 5. Restrições
5.1. É proibido conceder acesso privilegiado a um prestador externo sem contrato e termo de confidencialidade vigentes.
5.2. É proibido elevar privilégio de uma conta de serviço (não humana) para uso interativo por pessoa.
5.3. É proibido acesso privilegiado permanente mesmo para o time de IAM. O próprio IAM usa o CyberArk.

## 6. Regra de leitura para o assistente
6.1. Pedido de acesso administrativo permanente: resposta NÃO PODE, cita o item 2.1, e orienta sessão temporária via CyberArk.
6.2. Pedido de acesso privilegiado com MFA por SMS: resposta NÃO PODE, cita o item 2.4.
6.3. Pedido de acesso privilegiado para prestador externo sem contrato: resposta NÃO PODE, cita o item 5.1.
6.4. Pedido de sessão privilegiada dentro das regras (janela, MFA forte, justificativa): resposta PRECISA APROVAÇÃO ADICIONAL (dono do recurso e gestor, item 3.3).
