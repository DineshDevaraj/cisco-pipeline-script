pipeline {
    agent any 
    stages {
        stage('get-contacts') {
            steps {
                script {

                    def username = input(
                        message:'enter the username', 
                        parameters:[
                            string(name:'username')
                        ]
                    )
                    
                    def operation = input(
                        message: "Choose the operation",
                        parameters: [
                            [
                                $class: "ChoiceParameterDefinition",
                                choices: ["Add", "Get", "Update", "Delete"].join('\n'),
                                name: 'operation'
                            ]
                        ]
                    )
                    
                    def response = ""
                    
                    if (operation == "Add" || operation == "Update") {
                        
                        def fieldRecord = input(
                            message:'enter the field name and value', 
                            parameters:[
                                string(name:'fieldname'),
                                string(name:'fieldvalue')
                            ]
                        )
                        
                        response = sh(
                            script:"python3 /home/dinesh/programs/python/get-contact.py ${operation} ${username} ${fieldRecord.fieldname} ${fieldRecord.fieldvalue}", 
                            returnStdout:true
                        )
                        
                    } else {
                        
                        response = sh(
                            script:"python3 /home/dinesh/programs/python/get-contact.py ${operation} ${username}", 
                            returnStdout:true
                        )
                        
                    }
                    
                    def (key, value) = response.split(":")
                    if (key == "result") {
                        def (emailId, mobile, work) = value.split(";")
                        print("contact details for ${username} is ")                    
                        print("emailId : ${emailId}")
                        print("mobile : ${mobile}")
                        print("work : ${work}")
                    } else {
                        print(value)
                    }
                    
                }
            }
        }
    }
}
