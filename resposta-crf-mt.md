# Proposta técnica preliminar — Plataforma de formulários eletrônicos online

**Referência:** Pesquisa de Mercado nº 001/2026/CRF-MT — Levantamento para desenvolvimento de plataforma de formulários eletrônicos online do CRF-MT.

**Proponente:** Z F WEB TECH LTDA  
**CNPJ:** 63.119.849/0001-07  
**Local:** Brasília — DF  
**Contato (proponente):** contato.zfwebtech@gmail.com  

**Destinatário:** Conselho Regional de Farmácia do Estado de Mato Grosso — CRF-MT  
**Contato (conforme documento de pesquisa):** alex@crfmt.org.br  

**Data:** 02 de junho de 2026  

---

## Sobre valores, prazos e estimativas

**Os valores monetários, prazos detalhados e demais estimativas quantitativas permanecem intencionalmente vagos ou condicionados a premissas**, em razão das **lacunas de definição** ainda existentes no escopo — inclusive as apontadas na seção “Observações e questionamentos sobre acesso aos formulários” deste documento. Qualquer número apresentado nesta fase seria especulativo e poderia induzir expectativas incompatíveis com a realidade do projeto após o levantamento formal de requisitos, definição de modelo de acesso, volume de usuários, hospedagem e integrações. A proponente compromete-se a **refinar prazos e custos** assim que o CRF-MT **sanar as lacunas** ou formalizar premissas mínimas para dimensionamento.

---

## 1. Apresentação resumida da solução proposta

Propomos uma **aplicação web monolítica** centrada em **formulários dinâmicos**, perfis de atendimento (**Pessoa Física** e **Pessoa Jurídica**), **validações** e **regras de negócio** por serviço, **preenchimento responsivo** (desktop e mobile), **auditoria** e **conformidade com a LGPD**, com **geração automática de PDF** no padrão institucional do CRF-MT e **exportação de dados** para fins gerenciais e administrativos.

A solução será desenvolvida com **frontend em React.js**, **backend em .NET** e **banco de dados PostgreSQL**, hospedada em ambiente a definir conforme **volume de usuários**, disponibilidade e política de segurança do CRF-MT.

---

## 2. Arquitetura recomendada

| Camada | Tecnologia | Observação |
|--------|------------|------------|
| Interface | **React.js** | SPA ou SSR conforme decisão de SEO/integração com portal; componentes reutilizáveis para campos comuns entre formulários. |
| API e regras de negócio | **.NET** (ASP.NET Core) | Monólito modular: um deploy, módulos internos por domínio (cadastro, formulários, PDF, relatórios, administração). |
| Persistência | **PostgreSQL** | Dados transacionais, metadados de formulários, trilhas de auditoria e exportações. |
| Geração de PDF | Serviço no mesmo monólito ou biblioteca integrada | Templates alinhados aos PDFs atuais; versionamento de modelos. |

**Justificativa da arquitetura monolítica:** o escopo é predominantemente **formulários, validações, PDF e integrações pontuais**, sem necessidade imediata de microsserviços; isso **reduz complexidade operacional**, custo de infraestrutura e tempo de implantação, mantendo possibilidade de **evolução futura** (extração de módulos ou APIs dedicadas) se o volume ou a governança do CRF-MT exigirem.

---

## 3. Tecnologia sugerida para o desenvolvimento

- **Frontend:** React.js (TypeScript recomendado para robustez e manutenção).  
- **Backend:** .NET (ASP.NET Core), APIs REST, autenticação/autorização integrada ao monólito.  
- **Banco:** PostgreSQL.  
- **Integração com portal WordPress:** consumo de APIs do sistema de formulários (links “preencher online” no WordPress redirecionando ou incorporando iframe/SSO, conforme política de segurança) ou publicação de endpoints estáveis documentados (OpenAPI).  
- **Integrações externas:** exposição e consumo de APIs (HTTP/JSON), filas ou jobs internos para processamentos assíncronos (ex.: geração de PDF em lote), conforme necessidade levantada em fase de requisitos.

**Justificativa técnica resumida:** .NET + PostgreSQL oferecem desempenho, maturidade em ambiente corporativo e público, bom suporte a transações e auditoria; React.js facilita interfaces dinâmicas por serviço e reutilização de componentes entre os muitos formulários listados no Anexo I da pesquisa.

---

## 4. Funcionalidades alinhadas ao documento de pesquisa

- Seleção de perfil (**PF/PJ**) e **catálogo dinâmico de serviços** por perfil.  
- Formulários **responsivos**, validação de **campos obrigatórios** e **regras específicas** (horários, cargas horárias, consistências, alertas).  
- **Preenchimento assistido** com dados permitidos pelo CRF-MT, com registro de consentimento e minimização de dados (LGPD).  
- **Geração automática de PDF** final compatível com o fluxo administrativo atual.  
- **Exportação** para gestão (relatórios, CSV/Excel conforme política do órgão).  
- **Alertas e críticas** automáticas para inconsistências.  
- **Rastreabilidade e auditoria** (quem, quando, o quê, IP quando aplicável, versão do formulário).  
- Módulo de **administração** para versionamento de formulários, parâmetros e perfis de acesso (detalhamento depende das respostas à seção 6).

---

## 5. Requisitos mínimos de infraestrutura e banco (orientativos)

**Infraestrutura e definição de ambiente** dependem do **volume esperado de usuários concorrentes**, janelas de pico, SLA desejado e se o acesso será **somente internet** ou também **rede interna**.

Premissas típicas para dimensionamento inicial (a calibrar com o CRF-MT):

- **Aplicação:** serviço web (.NET) + armazenamento para PDFs e anexos (se houver).  
- **Banco:** PostgreSQL com backup, réplica ou ambiente de homologação conforme criticidade.  
- **Ambientes:** pelo menos **desenvolvimento**, **homologação** e **produção**; quantidade de réplicas em produção escala com carga.

Valores de CPU/RAM e custos de cloud **não são fixados nesta fase** sem métrica de concorrência e política de retenção de dados — alinhado à observação do início deste documento sobre **lacunas de definição**.

---

## 6. Estimativas preliminares (caráter orientativo e condicionado)

| Item | Observação |
|------|------------|
| **Prazo de desenvolvimento** | Depende do fechamento de requisitos (quantidade efetiva de formulários na 1ª onda, complexidade do “Requerimento do Estabelecimento” e escalas, integrações, SSO e retroativos). Mantém-se **vago em meses/semanas** até sanar lacunas. |
| **Custo de implantação** | Compõe-se de análise detalhada, implementação, testes, implantação, treinamento e documentação; **sem valor fechado** nesta manifestação, pelas mesmas **lacunas de definição**. |
| **Suporte e manutenção** | Contrato mensal ou horas técnicas, proporcional a SLA e evoluções; **estimativa numérica após** definição de escopo operacional. |

**Premissas para qualquer estimativa numérica futura:** quantidade de formulários na primeira entrega, necessidade de assinatura digital qualificada, volume de submissões/dia, retenção e anonimização, integrações com sistemas legados além do WordPress, e modelo de identidade (cadastro próprio vs. integração com provedor institucional).

---

## 7. Composição mínima sugerida da equipe técnica

- Product Owner / Analista de negócio (interface com áreas do CRF-MT).  
- Arquiteto/desenvolvedor backend .NET.  
- Desenvolvedor frontend React.js.  
- Especialista em UX/UI (formulários longos e acessibilidade).  
- QA / testes.  
- DevOps ou responsável por deploy e ambientes (conforme hospedagem definida).

Escalação opcional: DPO consultivo ou parecer jurídico-interno do CRF-MT para fluxos de dados sensíveis.

---

## 8. Experiências anteriores

*(Preencher pela Z F WEB TECH LTDA com casos reais: setor, tipo de sistema, stack, escopo e resultados — conforme item h da pesquisa de mercado.)*

---

## 9. Riscos e recomendações

- **Complexidade subestimada** em formulários com muitas regras (escalas, estabelecimento): mitigação com **priorização por ondas** e prova de conceito em 1–2 formulários críticos.  
- **Alinhamento PDF final** com identidade visual e campos legais: validação jurídica/administrativa do CRF-MT.  
- **LGPD:** bases legais, política de retenção, direitos do titular e registro de operações de tratamento.  
- **Dependências** de identidade única institucional (se existir): impacta prazo e arquitetura de login.

---

## 10. Observações e questionamentos sobre acesso aos formulários

Para fechar arquitetura de segurança, dimensionamento e contrato de serviço, solicitamos **esclarecimentos oficiais** do CRF-MT sobre:

1. **Usuários cadastrados:** os formulários serão preenchidos apenas por **usuários previamente cadastrados** no sistema (ex.: farmacêutico com vínculo ao registro), ou também haverá **fluxos anônimos** ou “convidados”?  
2. **Restrição de acesso:** além do login, haverá **restrição por perfil** (PF/PJ, RT, funcionário do CRF), por **serviço** ou por **vínculo com registro ativo**?  
3. **Controle de acesso:** é necessário **granularidade** (ex.: apenas visualizar rascunho vs. submeter; áreas internas do conselho vs. público externo)?  
4. **Gestão de autenticação e autorização:** o CRF-MT pretende **gestão própria** de usuários e papéis na aplicação, **integração com provedor** (Azure AD, Gov.br, LDAP interno, etc.) ou **modelo híbrido**?  
5. **Internet vs. intranet:** o acesso aos formulários será **exclusivamente pela internet**, **exclusivamente por intranet** (rede do CRF-MT) ou **ambos** (ex.: público externo + revisão interna)? Isso afeta firewall, VPN, certificados e auditoria.  
6. **Hospedagem da aplicação:** depende do **volume esperado de usuários** (concorrentes e diários), picos sazonais, necessidade de **redundância** e soberania de dados; a proponente detalha opções após esses números.  
7. **Definição de ambiente** (quantidade de servidores, réplicas, homologação/produção, DR): igualmente **depende do volume esperado**, RTO/RPO desejados e orçamento institucional.

Estas lacunas impactam **diretamente** custo, prazo e arquitetura de segurança — reforçando a deliberação expressa na seção inicial sobre **estimativas vagas** nesta fase.

---

## 11. Síntese (conforme solicitado no documento de pesquisa)

| Campo | Conteúdo |
|--------|----------|
| **Solução proposta** | Aplicação web monolítica de formulários dinâmicos com PDF institucional, auditoria e LGPD. |
| **Tecnologia recomendada** | React.js + .NET (ASP.NET Core) + PostgreSQL. |
| **Prazo estimado** | Vago/condicionado — refinamento após sanar lacunas de definição e escopo por ondas. |
| **Valor estimado — implantação** | Vago/condicionado — mesma razão; sem compromisso numérico nesta pesquisa de mercado. |
| **Valor estimado — manutenção/suporte** | Vago/condicionado — depende de SLA e volume de evoluções. |
| **Principais premissas** | Escopo por ondas, modelo de identidade, internet/intranet, volume de usuários, integrações WordPress/APIs, quantidade de formulários na primeira entrega e **respostas à seção 10**. |

---

**Declaração:** Esta manifestação destina-se exclusivamente ao **levantamento de mercado e planejamento** do CRF-MT, sem gerar obrigação contratual, nos termos do próprio documento de pesquisa.

**Z F WEB TECH LTDA** — CNPJ 63.119.849/0001-07 — Brasília/DF — contato.zfwebtech@gmail.com  
