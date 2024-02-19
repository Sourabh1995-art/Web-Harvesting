[UK_updated_Sourabh.csv](https://github.com/Sourabh1995-art/Web-Harvesting/files/14326874/UK_updated_Sourabh.csv)# Web-Harvesting
"Python (BeautifulSoup) for Uttarakhand hotel data extraction: EDA insights from Booking.com"

from bs4 import BeautifulSoup
import requests
import pandas as pd


headers={
    'User-Agent':'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/115.0.0.0 Safari/537.36',
    'Accept-Language' : 'en-US'
}


def pages_():
    url=input("Enter the Url here :  ") 
    response=requests.get(url,headers=headers)
    soup=BeautifulSoup(response.text,'html.parser')
    
    global hotels_data
    hotels=soup.findAll('div',{'data-testid':"property-card"})
    for hotel in hotels:
        #Extract hotel name
        name_element=hotel.find('div',{'data-testid':"title"})
        name=name_element.text.strip()
        #Price
        price_element=hotel.find('span',{'data-testid':"price-and-discounted-price"})
        price=price_element.text.strip()
        rating_element=hotel.find('div',{'class': 'a3b8729ab1 d86cee9b25'})
        #rating=rating_element.text.strip()
        rating=rating_element['aria-label'] if rating_element else 'NA'
        
        loc_element=hotel.find('span',{'data-testid': "address" })
        location=loc_element.text.strip()
        
        bdtype_element=hotel.find('span',{'class': 'df597226dd'})
        bed_type=bdtype_element.text.strip()
        rmsize_element=hotel.find('div',{'class': 'abf093bdfe f45d8e4c32'})
        room_size=rmsize_element.text.strip()
        noreview_element=hotel.find('div',{'class': 'abf093bdfe f45d8e4c32 d935416c47'})
        no_review=noreview_element.text.strip()
        #no_review=noreview_element['aria-label'] if rating_element else 'NA'
        #locUrl = hotel.find('span', {'class':'f4bd0794db b4273d69aa' })['href']

        hotels_data.append({
            'Name':name,
            'Price':price,
            'Ratings':rating,
            'Location':location,
            'Bedroom Type':bed_type,
            'Room Size':room_size,
            'No of Reviews':no_review,
            #'Map Location':locUrl


        })


def page_1():
    global hotels_data
    hotels_data = []
    pages_()

page_1()

pages_()

hotels_data

df  = pd.DataFrame(hotels_data)
df

df.shape

df.to_csv("Uttrakhand_dataset_new_Sourabh.csv")

Below I have presented some glimpses of my project in .png and .csv format


![Screenshot (50)](https://github.com/Sourabh1995-art/Web-Harvesting/assets/128116719/635c0ad3-1426-4462-9609-dfb1d311d232)
![Screenshot (48)](https://github.com/Sourabh1995-art/Web-Harvesting/assets/128116719/3a563066-4d11-4073-bd82-4f008b97e897)


![Screenshot (47)](https://github.com/Sourabh1995-art/Web-Harvesting/assets/128116719/c69990eb-a9ed-43ea-8bfe-8cb9b2015499)


[Uploading UK_updated_SUnnamed: 0,Name,Price,Ratings,Location,Bedroom Type,Room Size,No of Reviews
0,FabHotel Pramila Inn,"�1,414",8.1,Haridwar,8,16,291
1,"Aveo by Amatra, Gateway to Corbett","�2,800",8.4,Kashipur,0,3,106
2,"Mini Swiss, Harshil","�1,374",7.9,Harsil,10,10,15
3,Le ROI Floating Huts & Eco Rooms,"�4,500",7.5,Tehri,2,10,174
4,"Doon Valley Resort, Mussoorie",�845,6.6,Mussoorie,8,7,78
5,Itsy By Treebo - K K Residency Staywell,"�1,905",7.4,Roorkee,2,0,131
6,"Rama Guest House, Badrinath","�3,048",7.6,Badraina�th,5,0,18
7,"Hotel Kalash, Badrinath","�3,201",7.5,Badraina�th,10,16,21
8,Corbett Treat Resort,"�3,035",7.6,Ra�mnagar,4,3,118
9,Country Inn Nature Resort Bhimtal,"�4,720",7.9,Bhaim Ta�l,9,12,235
10,Munsyari The Roof Top,"�1,080",8.3,Munsyari,16,19,11
11,"Sravasti Inn Homestay, Uttarkashi","�1,672",7,Uttarka�shi,10,11,3
12,"Hotel Apex Heritage, Gangotri","�1,296",6.1,Gangotri,8,9,7
13,Himalaya View Resort,"�1,530",9.4,Barkot,17,19,7
14,"Lemon Tree Premier, Corbett","�7,500",8.2,Garjia,19,0,100
15,The Rosefinch Sarovar Portico,"�7,650",8.1,Bhaim Ta�l,14,10,239
16,"Amba Niwas Home Stay, Uttarkashi","�1,403",9.7,Uttarka�shi,10,18,26
17,Hotel Siddharth,�699,4.8,Tanakpur,17,17,55
18,Gomukh Hotel Uttarkashi,"�1,999",8.4,Uttarka�shi,2,19,24
19,Hotel Hari Ganga Haridwar - Near By Bus And Railway Station,�500,7.8,Haridwar,1,2,43
20,Taj Corbett Resort and Spa Uttarakhand,"�13,684",8.7,Ra�mnagar,20,10,412
21,Hyatt Centric Rajpur Road Dehradun,"�7,500",8.7,Dehradun,13,11,19
22,Treebo Trend Corbett Tiger Retreat,"�2,124",8.6,Ka�la�dhingi,2,1,13
23,Gomukh Home Stay,�899,7.4,Uttarka�shi,10,11,5
24,"Raj Palace, Uttarkashi","�2,057",8.3,Uttarka�shi,17,6,3
25,Onehouse Resort Lansdowne,"�2,310",8.5,Lansdowne,15,1,6
26,Nauling Paying Guest House,"�1,458",8,Dharamgarh,10,13,1
27,Jaseelo Camps,"�3,000",9.5,Chamba,21,1,2
28,"Doon Nature Valley Resort, Kempty Fall Mussoorie",�623,6.5,Mussoorie,15,3,49
29,"The Kempty Fall Resort, Mussoorie","�1,055",8.3,Mussoorie,8,9,61
30,"Rio Classic, Top Rated & Most Awarded Property in Haridwar","�1,150",7,Haridwar,8,9,8
31,"Hotel Pinerock & Cafe, Mussoorie - A Four Star Luxury Hotel","�1,071",5.6,Mussoorie,7,0,60
32,"Fortune Walkway Mall, Haldwani - Member ITC's Hotel Group","�6,750",8.8,Haldwa�ni,22,0,56
33,BSR Farms Resort,"�2,600",9.2,Pauri,12,17,36
34,Ganges blossam - A Four Star Luxury Hotel & Resort,"�1,606",9,Haridwar,6,5,9
35,Kaara Anantara Resort & Spa Jim Corbett,"�6,300",8.2,Ka�la�garh,11,4,6
36,"Sitara Hotel & Resort, ! Most Awarded Property in Mussoorie","�1,599",9.7,Mussoorie,3,19,3
37,"Nature Heaven Lodge, Mussoorie","�1,500",8.5,Mussoorie,3,5,6
38,Hotel North House,"�3,299",8.1,Haldwa�ni,8,15,99
39,"Hotel Pine Rock Mountain View, Mussoorie","�1,599",9.1,Mussoorie,8,4,10
40,"Bamboo Junction Resort - Kanatal, Valley & Mountain View","�2,080",8.4,Dhanaulti,3,13,12
41,"The Rio Lodge, Haridwar","�1,500",8.7,Haridwar,17,9,112
42,"Aveo by Amatra, Gateway to Corbett","�2,800",8.4,Kashipur,0,4,106
43,"Hotel Vista Bhowali, Nainital - Vegetarian","�1,777",8,Bhowa�li,2,12,66
44,Nainital Homes,"�1,874",9.8,Bhowa�li,12,9,52
45,"Hotel Kempty - A Boutique Hotel, Mussoorie","�1,519",7.9,Mussoorie,20,10,11
46,"Nature Valley Resort, Mussoorie - By Sitara Group","�1,125",8.7,Mussoorie,13,11,57
47,"Mini Swiss, Harshil","�1,374",7.9,Harsil,10,0,15
48,"The Southern Soul, Mussoorie","�3,500",9.7,Mussoorie,3,17,4
49,The Woods Retreat,"�10,000",8.5,Lansdowne,18,6,19
ourabh.csv…]()
