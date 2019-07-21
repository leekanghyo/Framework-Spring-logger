# Framework-Spring-logger

<p>
  Custom logger settings in Spring project
  
  This is a note on the custom log class using Log4j in Spring MVC.<br>
  The Log4j utility is automatically included when you create a Spring project.
  If you have a development environment that does not automatically include Log4j, you will need to add it separately.<br><br>
  Class names and file names used names that I use often.
  Therefore, when using this information, you need to change the class name and file name.
  <br><br>
  <img src="https://user-images.githubusercontent.com/47176449/61588335-bfc0a280-abd4-11e9-9f27-04ed7b85f5cb.PNG">
  <img src="https://user-images.githubusercontent.com/47176449/61588336-c222fc80-abd4-11e9-8200-9266842ff666.PNG">
</p>
<br>
<br>
<h2>Files Setting Info</h2>
<h3>[servelt-context.xml - set context component scan java class]</h3>

    <context:component-scan base-package="com.overload" />

<h3></h3>
<h3>[web.xml - context mapping set... add file - applicationContext*.xml]</h3>

    <context-param>
        <param-name>contextConfigLocation</param-name>
        <param-value>/WEB-INF/spring/root-context.xml, /WEB-INF/spring/applicationContext*.xml</param-value>
    </context-param>

<h3>[WEB-INF > spring > Your Context.xml - set (ex: applicationContext-manager.xml)]</h3>
  
  	<bean
        id="applicationManager"
        class="com.overload.application.ApplicationManager"
        init-method="start"
        destroy-method="stop">
    </bean>

<h3>[java Resources > src/main/java > Your java class (ex: ApplicationManager.java)]</h3>
    
    package com.overload.application;
    
    import java.text.SimpleDateFormat;
    import java.util.Date;
    
    import org.slf4j.Logger;
    import org.slf4j.LoggerFactory;

    public final class ApplicationManager {

          private Logger log = LoggerFactory.getLogger(this.getClass());

          // server state log
          private String startTime = "";

          public void start() {
            SimpleDateFormat sd = new SimpleDateFormat("yyyy.MM.dd HH:mm:ss");
            startTime = sd.format(new Date());

            if (log.isInfoEnabled()) {
              log.info("====================================================");
              log.info("=			[Overload] Program Start			=");
              log.info("====================================================");
              log.info("");
            }
	}

          public void stop() {

            if (log.isInfoEnabled()) {
              log.info("");
              log.info("====================================================");
              log.info("=			[Overload] Program Stop			=");
              log.info("====================================================");
            }
          }

          public String getStartTime() {
            return startTime;
          }

    }
