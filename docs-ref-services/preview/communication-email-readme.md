---
title: Azure Communication Email client library for JavaScript
keywords: Azure, javascript, SDK, API, @azure/communication-email, communication
author: petrsvihlik
ms.author: petrsvihlik
ms.date: 05/24/2022
ms.topic: reference
ms.devlang: javascript
ms.service: communication
---
# Azure Communication Email client library for JavaScript - Version 1.0.0-beta.1 


This package contains a JavaScript/TypeScript SDK for Azure Communication Services for Email.

## Getting started

### Prerequisites

You need an [Azure subscription][azure_sub], a [Communication Service Resource][communication_resource_docs], and an [Email Communication Resource][email_resource_docs] with an active [Domain][domain_overview].

To create these resource, you can use the [Azure Portal][communication_resource_create_portal], the [Azure PowerShell][communication_resource_create_power_shell], or the [.NET management client library][communication_resource_create_net].

### Installing

```bash
npm install @azure/communication-email
```

### Browser support

## Key concepts

`EmailClient` provides the functionality to send email messages .

## Examples

## Authentication

Email clients can be authenticated using the connection string acquired from an Azure Communication Resource in the [Azure Portal][azure_portal].

```typescript
import { EmailClient } from "@azure/communication-email";

const connectionString = `endpoint=https://<resource-name>.communication.azure.com/;accessKey=<Base64-Encoded-Key>`;
const client = new EmailClient(connectionString);
```

## Examples

### Send an Email Message

To send an email message, call the `send` function from the `EmailClient`.

```typescript Snippet:Azure_Communication_Email_Send
const emailMessage: EmailMessage = {
  sender: "sender@contoso.com",
  content: {
    subject: "This is the subject",
    plainText: "This is the body",
  },
  recipients: {
    to: [
      {
        email: "customer@domain.com",
        displayName: "Customer Name",
      },
    ],
  },
};

const response = await emailClient.send(emailMessage);
```

### Send an Email Message to Multiple Recipients

To send an email message to multiple recipients, add a object for each recipient type and an object for each recipient.

```typescript Snippet:Azure_Communication_Email_Send_Multiple_Recipients
const emailMessage: EmailMessage = {
  sender: "sender@contoso.com",
  content: {
    subject: "This is the subject",
    plainText: "This is the body",
  },
  recipients: {
    to: [
      {
        email: "customer1@domain.com",
        displayName: "Customer Name 1",
      },
      {
        email: "customer2@domain.com",
        displayName: "Customer Name 2",
      },
    ],
    cC: [
      {
        email: "ccCustomer1@domain.com",
        displayName: " CC Customer 1",
      },
      {
        email: "ccCustomer2@domain.com",
        displayName: "CC Customer 2",
      },
    ],
    bCC: [
      {
        email: "bccCustomer1@domain.com",
        displayName: " BCC Customer 1",
      },
      {
        email: "bccCustomer2@domain.com",
        displayName: "BCC Customer 2",
      },
    ],
  },
};

const response = await emailClient.send(emailMessage);
```

### Send Email with Attachments

Azure Communication Services support sending email with attachments.

```typescript Snippet:Azure_Communication_Email_Send_With_Attachments
const filePath = "C://readme.txt";

const emailMessage: EmailMessage = {
  sender: "sender@contoso.com",
  content: {
    subject: "This is the subject",
    plainText: "This is the body",
  },
  recipients: {
    toRecipients: [
      {
        email: "customer@domain.com",
        displayName: "Customer Name",
      },
    ],
  },
  attachments: [
    {
      name: path.basename(filePath),
      attachmentType: "txt",
      contentBytesBase64: readFileSync(filePath, "base64"),
    },
  ],
};

const response = await emailClient.send(emailMessage);
```

### Get Email Message Status

The result from the `send` call contains a `messageId` which can be used to query the status of the email.

```typescript Snippet:Azure_Communication_Email_GetSendStatus
const messageId = await emailClient.send(emailMessage);

const status = await emailClient.getSendStatus(messageId);
```

## Next steps

- [Read more about Email in Azure Communication Services][nextsteps]

## Contributing

This project welcomes contributions and suggestions. Most contributions require you to agree to a Contributor License Agreement (CLA) declaring that you have the right to, and actually do, grant us the rights to use your contribution. For details, visit [cla.microsoft.com][cla].

This project has adopted the [Microsoft Open Source Code of Conduct][coc]. For more information see the [Code of Conduct FAQ][coc_faq] or contact [opencode@microsoft.com][coc_contact] with any additional questions or comments.

<!-- LINKS -->

[azure_sub]: https://azure.microsoft.com/free/dotnet/
[azure_portal]: https://portal.azure.com
[cla]: https://cla.microsoft.com
[coc]: https://opensource.microsoft.com/codeofconduct/
[coc_faq]: https://opensource.microsoft.com/codeofconduct/faq/
[coc_contact]: mailto:opencode@microsoft.com
[communication_resource_docs]: /azure/communication-services/quickstarts/create-communication-resource?tabs=windows&pivots=platform-azp
[email_resource_docs]: https://aka.ms/acsemail/createemailresource
[communication_resource_create_portal]: /azure/communication-services/quickstarts/create-communication-resource?tabs=windows&pivots=platform-azp
[communication_resource_create_power_shell]: /powershell/module/az.communication/new-azcommunicationservice
[communication_resource_create_net]: /azure/communication-services/quickstarts/create-communication-resource?tabs=windows&pivots=platform-net
[package]: https://www.nuget.org/packages/Azure.Communication.Common/
[product_docs]: https://aka.ms/acsemail/overview
[nextsteps]: https://aka.ms/acsemail/overview
[nuget]: https://www.nuget.org/
[source]: https://github.com/Azure/azure-sdk-for-net/tree/main/sdk/communication
[domain_overview]: https://aka.ms/acsemail/domainsoverview

