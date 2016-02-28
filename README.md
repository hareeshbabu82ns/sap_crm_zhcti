# SAP CRM - Computer Training Institue

SAP CRM Case Study for CTI (Computer Training Institue), which consists Courses, Trainers, Trainees management etc..

#### For Installing code into SAP instance, Please follow instructions as in [HSAPLink](https://github.com/hareeshbabu82ns/hsaplink)

# Configuration

* SM34 - CRMVC_GIL_APPDEF
* Compnent - ZCTI

| Title | Config Entry |
| ----- | ------ |
| Implementation Class | **ZCTI_CL_MODEL_IL** |
| Object Table | **ZCTI_DB_ALLOB_IL** |
| Model Table | **ZCTI_DB_MODEL_IL** |

* Component Set - **ZCTI**
  * Include Components ZCTI
* Object Table **ZCTI_DB_ALLOB_IL**
  * will provide all GenIL objects within Component ZCTI
  * will be constructed as subset of fields of **CRMT_OBJ_PROPERTIES_TAB**

| Object Name | Kind | Root | Attribute St. | Key St. | Create St. | Result Object | Object Handler |
|---|---|---|---|---|---|---|---|
|**CTICourse**| A - Root||ZCTI_ST_COURSE_ATTR|ZCTI_ST_COURSE_KEY|ZCTI_ST_COURSE_CREATE||ZCTI_CL_COURSE|
|**CTICourseSearch**| D - Search|CTICourse|ZCTI_ST_COURSE_SEARCH|||CTICourse|ZCTI_CL_COURSE|

* Model Table **ZCTI_DB_MODEL_IL**
  * will provide all GenIL Objects Relations within Component ZCTI
  * will be constructed as subset of fields of **CRMT_RELATION_DETAIL_TAB**

| Object A | Relation | Object B | Cardinality A | Cardinality B | Relation Kind |
|---|---|---|---|---|---|
|**--**|--|--|--|--|--|

* Implementation Class **ZCTI_CL_MODEL_IL**
  * must inherit from
    * **CL_CRM_GENIL_ABSTR_COMPONENT** for objects with KEY as only **GUID**
    * **CL_CRM_GENIL_ABSTR_COMPONENT2** for objects with KEY other than **GUID**

| Method Redefined | Usage |
|---|---|
|**GET_OBJECT_PROPS**| provides available objects for Component ZCTI using **ZCTI_DB_ALLOB_IL**|
|**GET_MODEL**| provides object relations for Component ZCTI using **ZCTI_DB_MODEL_IL**|
|**GET_QUERY_RESULT**| this is a simple query, where we need to fetch Object Keys from buffer/db based on **IT_PARAMETERS** and put into **IV_ROOT_LIST**, which will call **GET_OBJECTS** to fetch attributes|
|**GET_OBJECTS**|fetch object attributes from buffer/db and set into **IT_ROOT_OBJECTS**|
|**SAVE_OBJECTS**|loop through **CT_OBJECT_LIST** and save objects to DB, update the status into **LINE-SUCCESS**|
|**CREATE_OBJECTS**|create objects using **IV_PARAMETERS** and add KEYS into **IV_ROOT_LIST**|
|**MODIFY_OBJECTS**|loop through **IV_ROOT_LIST** objects and update buffers, when done updating add the final updated object keys to **ET_CHANGED_OBJECTS**|
|**DELETE_OBJECTS**|delete objects from buffer/db in **CT_OBJECT_LIST** and set **LINE-SUCCESS** to true.|
|**INIT_OBJECTS**|to reset the API buffers in **CT_OBJECT_LIST** and set **LINE-SUCCESS** to true.|
|**LOCK_OBJECTS**|to lock the root objects from **CT_OBJECT_LIST** and set **LINE-SUCCESS** to true.|

## Milestone
| Nugget(ddmmyyyy) | Description |
|----|----|
|ZCRM_CTI_28022016| Course CRUD |
