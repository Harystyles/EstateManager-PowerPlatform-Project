# Go to the UserGuide file 

[Check out the User guide file](https://github.com/Harystyles/EstateManager/blob/main/UserGuideEstateManager.pdf)!


## Power Automate Cloud Flows

The function used is called the Power Fx, and this was used in various parts of the application to achieve the needed behaviours.

The function below was used to validate the user's data before previewing the record, and eventually updating it in SharePoint 

#### Function is written on the "Visible" property
----
```Power Fx
Switch(
    true,
    IsBlank(WorkOrderFullNameTxt.Text), Notify("Please enter full name", NotificationType.Error),
    WorkOrderCompanyCombo.SelectedText.Value = "Select Company", Notify("Please select the appropriate company", NotificationType.Error),
    WorkOrderDptCombo.SelectedText.Value = "Select Department", Notify("Please select the appropriate department", NotificationType.Error),
    IsBlank(WorkOrderWorkLocationCombo.SelectedText.Value), Notify("Please select work location", NotificationType.Error),
    WorkOrderWorkLocationCombo.SelectedText.Value = "Select Location", Notify("Please select the appropriate location", NotificationType.Error),
    IsBlank(WorkOrderRequestCategoryCombo.SelectedText.Value), Notify("Please select category of request", NotificationType.Error),
    WorkOrderRequestCategoryCombo.SelectedText.Value = "Select Request Category", Notify("Please select the appropriate request category", NotificationType.Error),
    IsBlank(WorkOrderQtyTxt.Text), Notify("Please enter quantity", NotificationType.Error),
    WorkOrderPreferredCloseOutDatePicker.SelectedDate < WorkOrderRequestedDatePicker.SelectedDate, Notify("Close out date must be after the requested date", NotificationType.Error),
    IsBlank(WorkOrderRequestDetailsTxt.Text), Notify("Please provide details of your request", NotificationType.Error),
    Navigate(
        'Facility Maintenance Review Screen',
        ScreenTransition.CoverRight,
        {
            PreWorkOrderFullName: WorkOrderFullNameTxt.Text,
            PreWorkOrderDpt: WorkOrderDptCombo.Selected,
            PreWorkOrderLocation: WorkOrderWorkLocationCombo.Selected,
            PreWorkOrderRequestCategory: WorkOrderRequestCategoryCombo.Selected,
            PreWorkOrderCompany: WorkOrderCompanyCombo.Selected,
            PreWorkOrderQty: WorkOrderQtyTxt.Text,
            PreWorkOrderRequestedDate: WorkOrderRequestedDatePicker.SelectedDate,
            PreWorkOrderPreClosedOutDate: WorkOrderPreferredCloseOutDatePicker.SelectedDate,
            PreWorkOrderRequestDetails: WorkOrderRequestDetailsTxt.Text
        }
    )
);
```
## Testing and Go-Live
### Write, organize, and automate tests for canvas apps, then deploy

The following processes were taken during the testing exercise.

_kindly note that this process is not in the order listed_

- Unit Test: To write tests using Power Apps expressions and to test all functionalities in a web browser
- Monitor: To trace events as they occur in a canvas app during the authoring experience in Power Apps Studio. It was also used Monitor to debug the published version of a canvas app
- Beta testing: Engaged potential users to use the app before its lunch
- User Acceptance Test: Presented a demo session to engage the sponsors of the app
- Change Management: Demo the app to the technical team and handover to the support team
  
----
