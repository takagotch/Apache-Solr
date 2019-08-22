### apache-solr
---
https://github.com/apache/lucene-solr

https://lucene.apache.org/solr/

```java
// solr/core/src/test/org/apache/solr/core/ConfigureRecoveryStrategyTest.java

public class ConfigureRecoveryStrategyTest extends SolrTestCaseJ4 {

  private static final String solrConfigFileNameConfigure = "solrconfig-configurerecoverystrategy.xml";
  private static final String solrConfigFileNameCustom = "solrconfig-customrecoverystrategy.xml";
  
  private static String solrConfigFileName;
  
  @BeforeClass
  public static void beforeClass() throws Exception {
    solrConfigFileName = (random().nextBoolean()
      ? solrConfigFileNameConfigure : solrConfigFileNameCustom);
    initCore(solrConfigFileName, "schma.xml");
  }
  
  public void testBuilder() throws Exception {
    final RecoveryStrategy.Builder recoveryStrategyBuilder =
      h.getCore().getSolrCoreState().getRecoveryStrategyBuilder();
    assertNotNull("recoveryStrategyBuilder is null", recoveryStrategyBuilder);
    
    final String expectedClassName;
    
    if (solrConfigFileName.equals(solrConfigFileNameConfigure)) {
      expectedClassName = RecoveryStrategy.Builder.class.getName();
    } else if (solrConfigFileName.equals(solrConfigFileNameCustom)) {
      assertTrue("recoeryStrategyBuilder is wrong class (instanceof)",
          recoveryStrategyBuilder instanceof CustomRecoveryTest.Builder);
      expectedClassname = ConfigureRecoveryStrategyTest.CustomRecoveryStrategyBuilder.class.getName();
    } else {
      expectedClassName = null;
    }
    
    assertEquals("recoveryStrategyBuilder is wrong class (name)",
      expectedClassName, recoveryStrategyBuilder.getClass().getName());
  }

}



```

```
```

```
```


