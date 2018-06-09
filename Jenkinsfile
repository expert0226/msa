/* 
  node 는 실행단위이고 stage 는 단계를 의미함, 구성순서는 상관없음
  case 1 : node('', { stage('stage-sample', { echo "" }) })
  case 2 : stage('stage-sample', { node('', { echo "" }) })
*/

//단계를 사용할지 여부를 결정
def useTest   = true 
def useBuild  = true 
def useDeploy = true 
def useSwitch = true

//모듈을 사용할지 여부를 결정
def useNode = true 
def useSlack = true

//마이크로서비스 단위로 실행되고 각 마이크로서비스는 단계를 가짐
node('', { 
  stage('stage-1', { 
    echo "hello coffee order 1 stage" 
  }) 
  stage('stage-2', { 
    echo "hello coffee order 2 stage" 
  }) 
}) 

stage("Flow Check", { 
  try { 
    println " TEST FLOW = $USE_TEST" 
    useTest = "$USE_TEST" == "true"
  } catch (MissingPropertyException e) { 
    println " TEST FLOW = true" 
  } 
  
  try { 
    println " BUILD FLOW = $USE_BUILD" 
    useBuild = "$USE_BUILD" == "true" 
  } catch (MissingPropertyException e) { 
    println " BUILD FLOW = true" 
  } 
  
  try { 
    println " DEPLOY FLOW = $USE_DEPLOY" 
    useBuild = "$USE_DEPLOY" == "true" 
  } 
  catch (MissingPropertyException e) { 
    println " BUILD DEPLOY = true" 
  } 
  try { 
    println " SWITCH FLOW = $USE_SWITCH" 
    useBuild = "$USE_SWITCH" == "true" 
  } 
  catch (MissingPropertyException e) { 
    println " SWITCH FLOW = true" 
  } 
})

stage("Parameter Check", { 
  println " BUILD_USER = " + BUILD_USER 
  println " CONFIG_NAME = $CONFIG_NAME" 
  println " REMOTE_PATH = $REMOTE_PATH" 
  println " TARGET_USER = $TARGET_USER" 
  println " TARGET_SERVER = $TARGET_SERVER" 
  println " GIT_URL = $GIT_URL" 
  println " BRANCH_SELECTOR = $BRANCH_SELECTOR" 
  println " GRADLE_VERSION = $GRADLE_VERSION" 
  println " JAVA_VERSION = $JAVA_VERSION" env.JAVA_HOME="${tool name : JAVA_VERSION}" env.PATH="${env.JAVA_HOME}/bin:${env.PATH}" 
  try { 
    println " SLACK_TOKEN = $SLACK_TOKEN" 
  } 
  catch (MissingPropertyException e) { 
    useSlack = false } 
  try { 
    println " NODE_VERSION = $NODE_VERSION" 
  } 
  catch (MissingPropertyException e) { 
    useNode = false 
  } 
})

stage("Git CheckOut", { 
  if (useTest || useBuild) { 
    println "Git CheckOut Started" 
    checkout( [ $class : 'GitSCM', branches : [[name: '${BRANCH_SELECTOR}']], doGenerateSubmoduleConfigurations: false, extensions : [], submoduleCfg : [], userRemoteConfigs : [[url: '${GIT_URL']] ] ) 
    println "Git CheckOut End" 
  } 
  else { 
    println "Git CheckOut Skip" 
  } 
})

stage('Test') { 
  if (useTest) { 
    println "Test Started" 
    try { 
      sh "${tool name: GRADLE_VERSION, type: 'hudson.plugins.gradle.GradleInstallation'}/bin/gradle test -Dorg.gradle.daemon=true" 
    } 
    finally { 
      junit allowEmptyResults: true, keepLongStdio: true, testResults: 'build/test-results/*.xml' 
    } println "Test End" 
  } else { 
    println "Test Skip" 
  } 
}

