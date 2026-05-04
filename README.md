# 🔔 Salesforce — Alerta de Inatividade em Oportunidades

Flow automatizado no Salesforce que notifica vendedores sobre oportunidades abertas sem atividade há 7 dias.

## 📋 Visão Geral

| Campo | Detalhe |
|---|---|
| Tipo | Scheduled-Triggered Flow |
| Objeto | Opportunity |
| Frequência | Diária |
| Ação | Envio de e-mail automático para o Owner |

## 🔧 Componentes do Flow

```
[Iniciar - Agendado Diário]
        ↓
[Get Records - Buscar Oportunidades Inativas]
  Filtros:
  • IsClosed = False
  • LastActivityDate ≤ TODAY() - 7
        ↓
[Loop - Loop Oportunidades]
  Para cada oportunidade:
        ↓
  [Action - Enviar Alerta Inatividade]
  • Destinatário: Owner > Email
  • Assunto: "Oportunidade sem atividade há 7 dias"
        ↓
[Término]
```

## 🚀 Como Importar

1. Acesse **Setup → Flows → New Flow**
2. Selecione **Scheduled-Triggered Flow**
3. Configure o objeto **Opportunity** e frequência **Diária**
4. Recrie os elementos conforme o diagrama acima

## ⚙️ Recursos Criados

### Fórmula: `DataLimite`
```
Tipo: Date
Fórmula: TODAY() - 7
```

### Filtros do Get Records
```
IsClosed = False
LastActivityDate <= {!DataLimite}
Armazenar: Todos os registros
```

### Ação de E-mail
```
Destinatário: {!Loop_Oportunidades.OwnerId > Email}
Assunto: Oportunidade sem atividade há 7 dias
Corpo: Mensagem de alerta com nome da oportunidade
```

## 📌 Pré-requisitos

- Salesforce com Sales Cloud ou licença que inclua Flow Builder
- Permissão de administrador para criar Flows
- Usuários com e-mail configurado no perfil

## 💡 Customizações Sugeridas

- Alterar o período de inatividade (trocar `7` por outro valor na fórmula)
- Adicionar filtro por **Stage** específico (ex: apenas Negotiation)
- Incluir **Task automática** além do e-mail
- Enviar **notificação in-app** via Custom Notification

## 📄 Licença

MIT — livre para usar e adaptar.

---

Feito com ☁️ no Salesforce Flow Builder | Sem código | 100% nativo
