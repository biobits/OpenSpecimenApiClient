# OpenSpecimenApiClient
 A C# client library to query the [OpenSpecimen](https://www.openspecimen.org/) WebApi


## Installation
Add OpenSpecimenApiCLient.dll to your project.

## Usage
```c#
using OpenSpecimenApiClient;

// Create a SessionInfo to authenticate a user and get an apitoken
SessionInfo sessionInfo = new SessionInfo {
                LoginName = "UserNAme",
                Password = "pa55word",
                DomainName = "openspecimen"
            };

// Create a QueryInfo with your aql Query (see [here](https://openspecimen.atlassian.net/wiki/spaces/CAT/pages/104529939/Query))
QueryInfo queryInfo = new QueryInfo
            {
                Aql = "select Participant.id as \"$cprId\", Participant.ppid as \"Participant_ID\", Participant.regDate as \"Participant_Registration_Date\", Specimen.id as \"$specimenId\", CollectionProtocol.id as \"$cpId\", Specimen.label as \"Specimen_Label\", Specimen.type as \"Specimen_Type\", Specimen.tissueSite as \"Anatomic_Site\", Specimen.id as \"Identifier\", Specimen.lineage as \"Lineage\", Specimen.class as \"Specimen_Class\", Specimen.createdOn as \"Created_On\", Specimen.initialQty as \"Initial_Quantity\", Specimen.availableQty as \"Available_Quantity\", Specimen.concentration, Specimen.collectionStatus as \"Collection_Status\", Specimen.activityStatus as \"Activity_Status\", Specimen.availabilityStatus as \"Availability_Status\", CollectionProtocol.shortTitle as \"Collection_Protocol_ShortTitle\", CollectionProtocol.Title as \"Collection_Protocol_Title\" where  CollectionProtocol.id exists   limit 0, 2",
                WideRowMode = QueryInfoWideRowMode.DEEP,
                OutputColumnExprs = false
            };
// Create an ApiQuery Object by providing the url to the openspecimen api. By istantiating the ApiQuery you provide the SessionInfo to get authenticated
ApiQuery apiQuery = new ApiQuery(sessionInfo, "https://my.openspecimen.net/openspecimen/rest/ng");

// Execute the Query
var queryresult = apiQuery.ExecuteQuery(queryInfo).Result;