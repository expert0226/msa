//node 는 실행단위 (병렬수행)
//stage 는 단계 (단계적수행)
//구성순서는 상관없음

//마이크로서비스 별 단계
node('', { 
  stage('stage-1', { 
    echo "hello coffee order 1 stage" 
  }) 
  stage('stage-2', { 
    echo "hello coffee order 2 stage" 
  }) 
  stage('stage-3', { 
    echo "hello coffee order 3 stage" 
  }) 
}) 

def useTest   = true 
def useBuild  = true 
def useDeploy = true 
def useSwitch = true

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

/*
stage('example2', { 
  node('', { 
    echo "" 
  }) 
})
*/
