 // styles.css 

/* Author: Samuel Rodriguez Medina */
/* Date: 2025-03-02 */
/* Description: Basic styling for the project */

body {
    font-family: Arial, sans-serif;
    margin: 0;
    padding: 0;
    background-color: #f4f4f4;
}

h1 {
    color: #333;
    text-align: center;
}
RUN Gradle Project level
 buildscript {
    repositories {
        // Check that you have the following line (if not, add it):
        google()  // Google's Maven repository
        mavenCentral() // Include to import Plaid Link Android SDK
    }
    dependencies {
        // ...
    }
}
Build Gradle App level
android {
  defaultConfig {
    minSdkVersion 21 // or greater
  }
}

dependencies {
  // ...
  implementation 'com.plaid.link:sdk-core:<insert latest version>'
}
String clientUserId = "user-id";

LinkTokenCreateRequestUser user = new LinkTokenCreateRequestUser()
  .clientUserId(clientUserId)
  .legalName("legal name")
  .phoneNumber("6238501522")
  .emailAddress("samsrodrigiez@gmail.com");

LinkTokenCreateRequest request = new LinkTokenCreateRequest()
  .user(user)
  .clientName("Plaid Test App")
  .products(Arrays.asList(Products.AUTH))
  .countryCodes(Arrays.asList(CountryCode.US))
  .language("en")
  .webhook("https://example.com/webhook")
  .linkCustomizationName("default")
  .androidPackageName("com.plaid.example")

Response<LinkTokenCreateResponse> response = client()
  .linkTokenCreate(request)
  .execute();

String linkToken = response.body().getLinkToken();

LinkTokenConfiguration linkTokenConfiguration = new LinkTokenConfiguration.Builder()
    .token("LINK_TOKEN_FROM_SERVER")
    .build();

    private ActivityResultLauncher<PlaidHandler> linkAccountToPlaid = registerForActivityResult(new FastOpenPlaidLink(),
  result -> {
    if (result instanceof LinkSuccess) {
      /* handle LinkSuccess */
    } else {
      /* handle Link loop for awhile*/
    }
  }
);
plaidHandler = Plaid.create(this.getApplication(), linkTokenConfiguration);
linkAccountToPlaid.launch(plaidHandler);
LinkSuccess success = (LinkSuccess) result;

String publicToken = success.getPublicToken();
LinkSuccess.LinkSuccessMetadata metadata = success.getMetadata();
for (LinkAccount account : success.getAccounts()) {
  String accountId = account.getId();
  String accountName = account.getName();
  String accountMask = account.getMask();
  LinkAccountSubtype accountSubtype = account.getSubtype();
}
String institutionId = metadata.getInstitution().getId();
String institutionName = metadata.getInstitution().getName();
