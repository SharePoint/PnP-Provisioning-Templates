# Templates Publishing Guidelines
In this document you can find instructions about how to create a PnP Provisioning Template that will be shared with the world-wide community.

## Requirements
In order to publish your own templates in the SharePoint PnP Gallery there are some requirements that you need to satisfy.

- Every template has to be stored in a dedicated folder of this repository. The folder has to be created as a child of the business category that the template targets. The supported categories - at the time of this writing - are:
    - Accounting
    - Business
    - Collaboration
    - Development
    - Document Management
    - Human Resources
    - IT Management
    - Others
- The template has to be stored as a .PNP Open XML file. The .XML template files are not supported.
- The template, within the .XML template file stored in the .PNP package, requires the following attributes:
    - The _DisplayName_ attribute
    - The _ImagePreviewUrl_ attribute with the URL targeting an image file stored within the same folder in which you store the .PNP file. External image files are not supported for security reasons.
    - Some custom _Properties_ to declare the target platform for the template. Here you can see the expected properties:
        - PnP_Supports_SPO_Platform: true/false
        - PnP_Supports_SP2016_Platform: true/false
        - PnP_Supports_SP2013_Platform: true/false
- You have to provide a README.md file wthin the template folder. This file will be used as a detailed description of your templates and will be shared through the SharePoint PnP Templates Gallery web site. Any image included in the README.md file must reference contents included in the folder of the current template. Images retrieved from external domains/folders are not allowed. Hyperlinks to external domains, like the web site of the subject or company that is providing the template to the community, are allowed but will be validated during the template approval process. Any link to unsafe or non-trustable contents will prevent the publishing of the template.
- The .PNP Open XML files cannot include any binary file like .DLL, .EXE or any script file like .PS1, .CMD, etc. 

## Technical Instructions
Let's say that you have a site, which you want to use to create a PnP Provisioning Template for sharing in this repository.
First of all, you will need to use the *Get-SPOProvisioningTemplate* cmdlet to extract the template from the live site. Here you can see an example:

```PowerShell
Connect-SPOnline "https://<yourtenant>.sharepoint.com/sites/<SourceSiteUrl>/"
Get-SPOProvisioningTemplate -Out .\TemplateFile.pnp -PersistBrandingFiles
```

Moreover, you will need to configure the required properties at the template level. Here you can see an example that uses the *Set-SPOProvisioningTemplateMetadata* cmdlet.

```PowerShell
Set-SPOProvisioningTemplateMetadata -Path .\TemplateFile.pnp -TemplateDisplayName "Display Name for your template" -TemplateImagePreviewUrl "https://raw.githubusercontent.com/OfficeDev/PnP-Provisioning-Templates/master/RootFolder/<TemplateCategory>/<TemplateFolder>/TemplatePreview.png" -TemplateProperties @{"PnP_Supports_SPO_Platform"="True";"PnP_Supports_SP2016_Platform"="False";"PnP_Supports_SP2013_Platform"="False"}
```

In the previous example, we se the Display Name and the Image Preview URL of the template. Furthermore, we configure the template properties so that the template will target SharePoint Online only, and not SharePoint 2013 or 2016 on-premises.

## Submitting a Template
Once you have created a .PNP template file, adhering to the requirements illustrated in the previous section, you can create a Pull Request against the master branch of this repository, and submit your template for approval.
The PnP Core Team will validate your submission and, upon approval, the template will be merged into the main repository, becoming publicly available.

Thanks for sharing your templates with the world-wide community.

Sharing is caring!