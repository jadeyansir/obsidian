## 1、@CookieValue
```java
@ApiOperation(value = "导入文件")  
@PostMapping("/import")  
public RestResponse<ErrorMsg> importTapBond(  
        @ApiParam(name = "mUserId", value = "用户id") @CookieValue Long mUserId,  
        @ApiParam(name = "file", value = "上传文件") @RequestBody MultipartFile file) throws IOException {  
    ErrorMsg errorMsg = tapBondInfoService.importTapBond(mUserId, file);  
    return RestResponse.Success(errorMsg);  
}
```
## 2、通过HttpServletRequest来获取
```java
@Resource  
private HttpServletRequest httpServletRequest;
Arrays.stream(httpServletRequest.getCookies())  
            .filter(x -> Objects.equals(x.getName(), "userid")).map(Cookie::getValue).findFirst();  
    Long userId = userIdOptional.map(Long::valueOf).orElse(null);  
```
```java
@Resource  
private HttpServletRequest httpServletRequest;
Arrays.stream(httpServletRequest.getCookies())  
            .filter(x -> Objects.equals(x.getName(), "userid")).map(Cookie::getValue).findFirst();  
    Long userId = userIdOptional.map(Long::valueOf).orElse(null);  
@Override  
public ErrorMsg excelImportBondGlobalCoordinator(MultipartFile multipartFile) throws IOException {  
    ExcelImportResult<BondGlobalCoordinatorImportBO> importExcelResult = EasyExcelTemplateActuator.importExcel(multipartFile,  
            BondGlobalCoordinatorImportBO.class, this::checkBondGlobalCoordinatorBO, this::handleBondGlobalCoordinatorData);  
    return importExcelResult.getErrorMsg();  
}  
  
private void handleBondGlobalCoordinatorData(  
        List<BondGlobalCoordinatorImportBO> bondGlobalCoordinatorImportBOList, ErrorMsg errorMsg) {  
    Optional<String> userIdOptional = Arrays.stream(httpServletRequest.getCookies())  
            .filter(x -> Objects.equals(x.getName(), "userid")).map(Cookie::getValue).findFirst();  
    Long userId = userIdOptional.map(Long::valueOf).orElse(null);  
    List<InternationalPublicDictDO> publicDictDOList = publicDictionaryDAO.getPublicDictionaryByEnumList(CAPITAL_TYPE);  
    Map<String, Integer> publicDictMap =  
            publicDictDOList.stream().collect(Collectors.toMap(InternationalPublicDictDO::getParameterName  
                    , InternationalPublicDictDO::getParameterCode));  
    List<BondGlobalCoordinatorDO> bondGlobalCoordinatorDOList = new ArrayList<>();  
    for (BondGlobalCoordinatorImportBO bondGlobalCoordinatorImportBO : bondGlobalCoordinatorImportBOList) {  
        BondGlobalCoordinatorDO bondGlobalCoordinatorDO = new BondGlobalCoordinatorDO();  
        bondGlobalCoordinatorCopier.copy(bondGlobalCoordinatorImportBO, bondGlobalCoordinatorDO, null);  
        bondGlobalCoordinatorDO.setCapitalType(publicDictMap.get(bondGlobalCoordinatorImportBO.getCapitalTypeStr()));  
        bondGlobalCoordinatorDOList.add(bondGlobalCoordinatorDO);  
    }  
    saveOrUpdateBondGlobalCoordinatorList(bondGlobalCoordinatorDOList, userId);  
}
```
