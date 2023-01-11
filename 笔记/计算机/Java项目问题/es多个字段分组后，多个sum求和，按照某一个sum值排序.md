```java
private AbstractAggregationBuilder buildAggregationBuilderByComGroup() {  
    AggregationBuilder issueScaleDollarSum = AggregationBuilders.sum(DURATION_ISSUE_SCALE).field(ISSUE_SCALE_IN_USD);  
    AggregationBuilder maturityAmountDollarSum = AggregationBuilders.sum(DURATION_MATURITY_AMOUNT).field(MATURITY_AMOUNT_IN_USD);  
    AggregationBuilder netIssueAmountDollarSum = AggregationBuilders.sum(DURATION_NET_ISSUE_AMOUNT).field(NET_ISSUE_AMOUNT_IN_USD);  
    //统计每个主体类别下数量  
    AbstractAggregationBuilder statsPeriodTypeGroup = AggregationBuilders.terms(COM_UNI_CODE).field(COM_UNI_CODE).size(TEN_THOUSAND);  
    //获取其他值  
    TopHitsAggregationBuilder topHits = AggregationBuilders.topHits("topHits").size(1);  
    statsPeriodTypeGroup.subAggregation(topHits);  
    statsPeriodTypeGroup.subAggregation(issueScaleDollarSum);  
    statsPeriodTypeGroup.subAggregation(maturityAmountDollarSum);  
    statsPeriodTypeGroup.subAggregation(netIssueAmountDollarSum);  
    statsPeriodTypeGroup.subAggregation(PipelineAggregatorBuilders.bucketSort("sortInterval",   Lists.newArrayList(SortBuilders.fieldSort(DURATION_ISSUE_SCALE).order(SortOrder.DESC)));  
    return statsPeriodTypeGroup;  
}
```



JSON成对象 `.getSourceAsString()`

```java
if (Objects.nonNull(topHits) && (topHits instanceof InternalTopHits)) {  
    List<IntlBondIssueStatsEs> bondIssueStatsEsList = Arrays.stream(((InternalTopHits) topHits).getHits().getHits())  
            .map(x -> JSON.parseObject(x.getSourceAsString(), IntlBondIssueStatsEs.class)).collect(Collectors.toList());  
    intlBondIssueCouponBO.setIntlBondUniCodeAndCouponBOList(buildIntlBondUniCodeAndCouponBO(bondIssueStatsEsList));  
}
```