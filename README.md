# rest-Api
rest api
@RestResource(urlmapping='/createAccount/*')
//what is url we can give 3 rd party--https://ap.16.salesforce.com/service/apexrest/createAccount?name=kishor&ndustry=banking&fax=800
//https://ap.16.salesforce.com/service/apexrest/createAccount?&name=kishor&ndustry=banaking&fax=800
//
//request Sturucture
//https://ap.16.salesforce.com/service/apexrest/createAccount? +name=  +ndustry=   +fax=
global class REstservie 
{
         @HttpPost
    global static string Callme( string name, string phone, string Industry)
   {                             //we have to do respond so serlaixation
       System.JSONGenerator js = JSON.createGenerator(true);
       js.writeStartObject();
           try
           {
              Account acc=new Account();
                  acc.Name=Name;
                  acc.Phone=phone;
                  acc.Industry=Industry;
               insert acc;
               js.writeStringField('status','Success');
               js.writestringField('AccounId', acc.id);
           }
       catch (exception e)
       {
           js.writeStringField('status','Failed');
               js.writestringField('AccounId',e.getMessage()); 
       }
       
           
       js.writeEndObject();    
           string result=js.getAsString();
            return result;
       
   }
}
