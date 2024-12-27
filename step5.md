# Using Object Page Layout as a Detail Page (Sử dụng `Object Page Layout` làm trang chi tiết)

Thêm `sap.uxap.ObjectPageLayout` để hiển thị thông tin từng product

`ObjectPageLayout` cung cấp cho phép app dễ dàng hiển thị thông tin liên quan đến business object

Sau version 1.52, `sap.f.DynamicPage`. Điều này đảm bảo tính khả dụng của các tính năng SAP Fiori, chẳng hạn như điều hướng theo đường dẫn, tác vụ điều hướng và mở rộng/thu gọn tiêu đề bằng cách nhấn/nhấp vào khu vực tiêu đề hoặc bằng cách chọn các nút mũi tên có sẵn.`Object Page Headers`

`sap.uxap.ObjectPageLayout` cung cấp nội dung có cấu trúc chặt chẽ hơn bằng cách sử dụng thanh neo tùy chọn và chặn nội dung được gói trong các phần và phần phụ cấu trúc thông tin. Để biết thêm thông tin, hãy xem `Object Page Layout`.

![alt text](image.png)

```xml
<mvc:View
	xmlns="sap.uxap"
	xmlns:m="sap.m"
	xmlns:f="sap.f"
	xmlns:form="sap.ui.layout.form"
	xmlns:mvc="sap.ui.core.mvc">
	<ObjectPageLayout
		id="ObjectPageLayout"
		showTitleInHeaderContent="true"
		alwaysShowContentHeader="false"
		preserveHeaderStateOnScroll="false"
		headerContentPinnable="true"
		isChildPage="true"
		upperCaseAnchorBar="false">
	</ObjectPageLayout>
</mvc:View>
```

`sap.uxap.ObjectPageLayout`

```xml
<mvc:View
	xmlns="sap.uxap"
	xmlns:m="sap.m"
	xmlns:f="sap.f"
	xmlns:form="sap.ui.layout.form"
	xmlns:mvc="sap.ui.core.mvc">
	<ObjectPageLayout
		id="ObjectPageLayout"
		showTitleInHeaderContent="true"
		alwaysShowContentHeader="false"
		preserveHeaderStateOnScroll="false"
		headerContentPinnable="true"
		isChildPage="true"
		upperCaseAnchorBar="false">
		<headerTitle>
			<ObjectPageDynamicHeaderTitle>
				<actions>
					<m:ToggleButton
						text="Edit"
						type="Emphasized"/>
					<m:Button
						text="Delete"
						type="Transparent"/>
					<m:Button
						text="Copy"
						type="Transparent"/>
					<m:Button
						icon="sap-icon://action"
						type="Transparent"/>
				</actions>
			</ObjectPageDynamicHeaderTitle>
		</headerTitle>

	</ObjectPageLayout>
</mvc:View>
```

Thêm dynamic header `ObjectPageDynamicHeaderTitle` trong `headerTitle` aggregation trong `ObjectPageLayout`

````xml
<headerContent>
			<m:FlexBox wrap="Wrap" fitContainer="true" alignItems="Stretch">
				<f:Avatar
					displaySize="L"
					displayShape="Square"
					class="sapUiTinyMarginEnd">
				</f:Avatar>
				<m:VBox justifyContent="Center" class="sapUiSmallMarginEnd">
					<m:Label text="Main Category"/>
				</m:VBox>
				<m:VBox justifyContent="Center" class="sapUiSmallMarginEnd">
					<m:Label text="Subcategory"/>
				</m:VBox>
				<m:VBox justifyContent="Center" class="sapUiSmallMarginEnd">
					<m:Label text="Price"/>
				</m:VBox>
			</m:FlexBox>
		</headerContent>
```

Thêm content `headerContent` aggregation. Chúng tôi sử dụng `sap.f.Avatar` SAP Fiori được đề xuất display image

```xml
	<sections>
			<ObjectPageSection title="General Information">
				<subSections>
					<ObjectPageSubSection>
						<blocks>
							<form:SimpleForm
								maxContainerCols="2"
								editable="false"
								layout="ResponsiveGridLayout"
								labelSpanL="12"
								labelSpanM="12"
								emptySpanL="0"
								emptySpanM="0"
								columnsL="1"
								columnsM="1">
								<form:content>
									<m:Label text="Product ID"/>
									<m:Label text="Description"/>
									<m:Label text="Supplier"/>
								</form:content>
							</form:SimpleForm>
						</blocks>
					</ObjectPageSubSection>
				</subSections>
			</ObjectPageSection>

			<ObjectPageSection title="Suppliers">
				<subSections>
					<ObjectPageSubSection>
						<blocks>
							<m:Table
								id="suppliersTable"
								items="{path : 'products>/ProductCollectionStats/Filters/1/values'}">
								<m:columns>
									<m:Column/>
								</m:columns>
								<m:items>
									<m:ColumnListItem type="Navigation">
										<m:cells>
											<m:ObjectIdentifier text="{products>text}"/>
										</m:cells>
									</m:ColumnListItem>
								</m:items>
							</m:Table>
						</blocks>
					</ObjectPageSubSection>
				</subSections>
			</ObjectPageSection>
		</sections>
```


````
