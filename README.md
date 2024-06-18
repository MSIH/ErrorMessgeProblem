# ErrorMessgeProblem
A razor component using a Generic object model does not render Validation Message for invalid field.

This does not work

    <EditForm Context="editFormComponent" OnValidSubmit="@HandleValidSubmit" Model="@model">
    <DataAnnotationsValidator />
    <h4>Validation Summary</h4>
    <ValidationSummary />
    @foreach (var property in model.GetType().GetProperties())
    {
        var propertyValue = property.GetValue(model)?.ToString();
        <div class="row mb-3">
            <div class="col">
                <div class="form-group">
                    <input @onchange='((e) => HandleValueChanged(e, property.Name))'
                           type="text"
                           value=@propertyValue
                           class="form-control" />
                </div>
            </div>
        </div>
        <h5>Validation Message</h5>
        <ValidationMessage For=@(() => property.Name) />
    }


This works

     <EditForm Context="editFormComponent" OnValidSubmit="@HandleValidSubmit" Model="@book">
    <DataAnnotationsValidator />
    <h4>Validation Summary</h4>
    <ValidationSummary />

    <div class="form-group">
        <label for="title">Title</label>
        <InputText id="title" class="form-control" @bind-Value="@book.Title" />
        <ValidationMessage For="@(() => book.Title)" />
    </div>

    <hr />
    <div class="row mb-3">
        <div class="col">
            <div class="form-group">
                <input type="submit" value="Save" class="btn btn-primary" />
            </div>
        </div>
    </div>
    </EditForm>
