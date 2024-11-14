---
title: Translate documents in OneDrive
ms.author: mactra
author: MachelleTranMSFT
manager: jtremper
ms.reviewer: karlha
ms.date: 11/13/2024
audience: admin
ms.topic: conceptual
ms.service: one-drive
search.appverid: 
ms.collection: 
    - enabler-strategic
ms.localizationpriority:  medium
description: Learn about the document translation service in OneDrive.
---

# Translate documents in OneDrive

> [!NOTE]
> Through June 2025, you can try out document translation and other selected Microsoft Syntex services at no cost if you have [pay-as-you-go billing](/microsoft-365/syntex/syntex-azure-billing) set up. For details on how to get started and the limitations, see [Try out Microsoft Syntex and explore its services](/microsoft-365/syntex/promo-syntex).

OneDrive, powered by Microsoft Syntex, allows you to translate documents while preserving the original format and structure. With this feature, you can create a translated copy of a single file or a set of files. The translation feature is available for all supported languages and dialects.

:::image type="content" source="media/onedrive-document-translation/1-onedrive-translation.png" alt-text="screenshot of OneDrive document translate feature." lightbox="media/onedrive-document-translation/1-onedrive-translation.png":::

---

## Key features

- **Manual or automatic translation**: You can manually translate files or set up a rule for automatic translation.
- **Translation of different file types**: Translate various file types, including .docx, .pdf, .pptx, and more.
- **Video transcripts and captions**: The translation feature also supports translating video transcripts and closed caption files. For more information, see [Transcript Translations in Stream for SharePoint](https://support.microsoft.com/office/microsoft-syntex-pay-as-you-go-transcript-translations-in-stream-for-sharepoint-2e34ad1b-e213-47ed-a806-5cc0d88751de).

---

## Requirements and limitations

### Supported file types

Document translation is available for the following file types:

- `.csv`, `.docx`, `.htm`, `.html`, `.markdown`, `.md`, `.msg`, `.pdf`, `.pptx`, `.txt`, `.xlsx`

For legacy file formats, the translated copy is created in the modern equivalent:

- `.doc` → `.docx`
- `.xls` → `.xlsx`
- `.ppt` → `.pptx`

> [!NOTE]
> SharePoint site pages are not supported for translation at this time.

### Supported file size

The maximum file size for translation is 40 MB.

### Supported languages

Translation in Syntex is available for all supported languages and dialects.

:::image type="content" source="media/onedrive-document-translation/2-onedrive-translation.png" alt-text="screenshot of OneDrive document translate feature with supported languages." lightbox="media/onedrive-document-translation/2-onedrive-translation.png":::

---

## Current limitations

- **Images**: Text embedded in images within documents isn't translated.
- **Encrypted files**: Encrypted files can't be translated.
- **Password-protected files**: Password-protected files aren't eligible for translation.
- **SharePoint libraries**: Translation actions are also available for files stored in SharePoint libraries.
- **On-demand translation for folders**: This feature will be available in a future release.

---

## Frequently asked questions

For more information, see the following resources:

- [Document Translation: FAQ](/azure/ai-services/translator/document-translation/faq#document-translation-faq)
- [How does Translator count characters?](/azure/ai-services/translator/translator-faq#how-does-translator-count-characters)
