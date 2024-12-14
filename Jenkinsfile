pipeline {
	agent any
	Tools {
		//maven 'Maven' // 'Maven' finns i inställningar > Tools. Namnet på din Tool i detta fall Maven läger du i.
	}
	parameters {
		// string(name: 'VERSION', defaultValue: '', description: 'version to deploy on prod')

		choice(name: 'VERSION', choices: ['1.1.0', '1.2.0', '1.3.0'], description: '')
		booleanparam(name: 'executeTests', defaultValue: true, description: '')
	}
	Environment {
		// Alla variabler jag skapar här kommer vara tillgängliga i alla stages under.
		NEW_VERSION = '1.3.0'
		SERVER_CREDENTIALS = credentials('demo-app-git-credentials') //Måste ladda ner credentials binding plugin. fyll i credentials ID't inom paranteserna.
	}	
	stages {
		stage ("build") {
			steps {
				// sh "mvn install"
				echo 'building the application...'
				echo "building version ${NEW_VERSION}"
				// echo 'building version ${NEW_VERSION}' kommer inte funka, måste använda "" om jag har med en variabel
			}
		}
		stage ("test") {
			when {
				expression {
					BRANCH_NAME == 'main' || BRANCH_NAME == 'master' //Kommer endast köras om current branch är main.
					params.executeTests
				}
			}
			steps {	
				
			}
		}
		stage ("deploy") {
			steps {
				echo 'deploying the application…'
				echo "deploying vesion ${VERSION}"
			}
		}
	}
	post {
		Always {
			//Kod som körs ALLTID
		}
		sucess {			
			//Kod som körs ENDAST om det lyckas
		}	
		failure {
			//Kod som körs ENDAST om det misslyckas
		}
	}
}
