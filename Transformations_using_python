# Transformations
Cleaning Data using Python 
mport pandas as pd
import numpy as np

marketing = pd.read_csv("bank_marketing.csv")
#creatings three variables for three tabels 
# Fixed column names: 'material' -> 'marital', 'eduactaion' -> 'education'
client = marketing[['client_id', 'age', 'job', 'marital', 'education', 'credit_default', 'mortgage']]

# Fixed typo: 'clinet_id' -> 'client_id'
# Removed 'last_contact_date' from the columns list, as it does not exist yet
campaign = marketing[['client_id','number_contacts','contact_duration','previous_campaign_contacts','previous_outcome','campaign_outcome','month','day']]

# Fixed typo: 'economis' -> 'economics'
economics = marketing[['client_id','cons_price_idx','euribor_three_months']]

# editing the client dataset 
client['education'] = client['education'].str.replace(".","_")
client['education'] = client['education'].replace("unknown",np.NaN)
client['job'] = client['job'].str.replace(".","_")
for col in ["credit_default","mortgage"]:
    client[col] = client[col].map({"yes": 1,"no": 0,"unknown": 0})
    client[col] = client[col].astype(bool)

#editing campaign data 
campaign['campaign_outcome'] = campaign['campaign_outcome'].map({"yes": 1,"no": 0})
campaign['previous_outcome'] = campaign['previous_outcome'].map({"success": 1,"failure":0,"nonexistent": 0})
campaign['year'] = '2022'
campaign['day'] = campaign['day'].astype(str)
# Now create 'last_contact_date' from the available columns
campaign['last_contact_date'] = campaign['year'] + '-' + campaign['month'] + '-' + campaign['day']
campaign['last_contact_date'] = pd.to_datetime(campaign['last_contact_date'], format = "%Y-%b-%d")
for col in ['campaign_outcome','previous_outcome']:
    campaign[col] = campaign[col].astype(bool)
campaign.drop(columns=['month','year','day'],inplace = True)

#editing 
client.to_csv("client.csv",index = False)
campaign.to_csv("campaign.csv",index = False)
economics.to_csv("economics.csv",index = False)
