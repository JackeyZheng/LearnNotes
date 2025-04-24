# Aurelius

### 在 TMS Aurelius 中，您可以使用以下方法来检查一个字段是否存在：
1. 使用 TMappingExplorer 类：您可以使用 TMappingExplorer 类的 FindField 方法来检查字段是否存在于映射中。这需要您有一个 TMappingExplorer 实例，并指定您感兴趣的字段名称。如果字段存在，则该方法将返回一个 TMappingField 对象，否则返回 nil。
这里 TMyEntity 是您感兴趣的实体类的类型，'FieldName' 是您要检查的字段名称。
2. 使用 RTTI（Run-Time Type Information）：您也可以使用 Delphi 的 RTTI 功能来检查类中是否存在指定的字段。这需要您使用 TRttiContext 类获取类的 RTTI 信息，然后检查字段是否存在。
这里的 TMyEntity 是您感兴趣的实体类的类型，'FieldName' 是您要检查的字段名称。
以上两种方法都可以帮助您确定指定的字段是否存在于类或映射中。

```pascal
uses
  Aurelius.Mapping;

var
  Explorer: TMappingExplorer;
  Field: TMappingField;
begin
  Explorer := TMappingExplorer.Create;
  try
    Field := Explorer.FindField(TMyEntity, 'FieldName');
    if Assigned(Field) then
      ShowMessage('Field exists!')
    else
      ShowMessage('Field does not exist!');
  finally
    Explorer.Free;
  end;
end;
uses
  System.Rtti, Aurelius.Mapping;

var
  Ctx: TRttiContext;
  EntityType: TRttiType;
  Field: TRttiField;
begin
  Ctx := TRttiContext.Create;
  try
    EntityType := Ctx.GetType(TMyEntity.ClassInfo);
    for Field in EntityType.GetFields do
    begin
      if Field.Name = 'FieldName' then
      begin
        ShowMessage('Field exists!');
        Exit;
      end;
    end;
    ShowMessage('Field does not exist!');
  finally
    Ctx.Free;
  end;
end;
```