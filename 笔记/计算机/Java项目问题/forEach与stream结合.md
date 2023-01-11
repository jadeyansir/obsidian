
issueStatsDOList.forEach(x -> {
                if (exchangeOfferIsinSet.contains(x.getIsin())) {
                    x.setBondIssueMethod(IssueMethodEnum.EXCHANGE_OFFER.getValue());
                }
            });
这种写法看起来很长
issueStatsDOList.stream().filter(x -> exchangeOfferIsinSet.contains(x.getIsin()))  
        .forEach(x -> x.setBondIssueMethod(IssueMethodEnum.EXCHANGE_OFFER.getValue()));

forEach传入的是一个Consumer，可以对集合中元素进行修改