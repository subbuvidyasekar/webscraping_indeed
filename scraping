 Title = []
 Rating = []
 Reviewer_designation = []
 Fulll_Location = []
 Date = []
 Comment = []
 Pros = []
 Cons = []
 Employee_Status = []
 Job_Title = []
 City = []
 State = []
 Company = []
        
comp_list = ['Company1','Company2','Company3']
        for c_name in comp_list:
            pages = [str(i) for i in list(range(0,600,20))]  
            for page in pages:
                print("Page :",page)
                url = 'https://www.indeed.com/cmp/'+c_name+'/reviews?fcountry=ALL&start='+page
                driver.get(url)
                overall_rating = driver.find_element_by_xpath('/html/body/div[2]/div/div[1]/header/div[2]/div[3]/div/div/div/div[1]/div[1]/div[2]/div[2]/div/div[2]/span[2]')
                for n in range(2,24,1):
                    if n != 6 and n != 12: 
                        #print("Number "+str(n))
                        title = driver.find_elements_by_xpath('/html/body/div[2]/div/div[1]/main/div[2]/div[1]/div/div['+str(n)+']/div/div[2]/h2/a/span/span/span')#'.//span[@class="css-hh75in-Box eu4oa1w0"]')#'/html/body/div[2]/div/div[1]/main/div[2]/div[1]/div/div')
                        comments = driver.find_elements_by_xpath('/html/body/div[2]/div/div[1]/main/div[2]/div[1]/div/div['+str(n)+']/div/div[2]/div[2]/span/span/span')
                        reviewers = driver.find_elements_by_xpath('/html/body/div[2]/div/div[1]/main/div[2]/div[1]/div/div['+str(n)+']/div/div[2]/div[1]/span')
                        user_ratings = driver.find_elements_by_xpath('/html/body/div[2]/div/div[1]/main/div[2]/div[1]/div/div['+str(n)+']/div/div[1]/div/button')
                        pros = driver.find_elements_by_xpath('/html/body/div[2]/div/div[1]/main/div[2]/div[1]/div/div['+str(n)+']/div/div[2]/div[3]/div/div[1]/div/span/span')
                        cons = driver.find_elements_by_xpath('/html/body/div[2]/div/div[1]/main/div[2]/div[1]/div/div['+str(n)+']/div/div[2]/div[3]/div/div[2]/div/span/span')
                        for ti,co,re, ur in zip(title,comments, reviewers, user_ratings):
                            Title.append(ti.text)
                            Comment.append(co.text)
                            rev_pos = re.text.replace("\n","")
                            splt = rev_pos.split('Employee) -') 
                            author = splt[0]+' Employee)'
                            #print(f"Author : {author}")
                            Reviewer_designation.append(author)
                            split_2 = splt[1].split('-')
                            #print(split_2)
                            if len(split_2)==3:
                                date1 = split_2[2] 
                                location = split_2[0]+","+split_2[1]
                            else:
                                date1 = split_2[1]
                                location = split_2[0]
                            #print(f"location : {location}")

                            Job_Title.append(author.split('(')[0])
                            if 'Current  Employee' in author:
                                Employee_Status.append("Current Employee")
                            else:
                                Employee_Status.append("Former Employee")                            
                           
                            Full_Location.append(location)
                            if(len(location.split(','))==1):
                                city = location.split(',')[0]
                                state = location.split(',')[0] 
                            else:
                                city= location.split(',')[0]
                                state = location.split(',')[1]
                            City.append(city)
                            State.append(state)

                            Date.append(date1)
                            Rating.append(float(ur.text))

                        if len(pros) != 0:
                            pr = pros[0].text
                        else:
                            pr = ' '
                        Pros.append(pr)
                        if len(cons) != 0:
                            cn = cons[0].text
                        else:
                            cn = ' '
                        Cons.append(cn)
                        Company.append(c_name)
                        

        comments = pd.DataFrame({'Reviewer_designation' : Reviewer_designation,
                                      'Job_Title' : Job_Title, 
                                      'Employee_Status' : Employee_Status,
                                      'City' : City,
                                      'State' : State,
                                      'Full_Location' : Full_Location,
                                      'Date' : Date,
                                      'Title' : Title,
                                      'Comment' : Comment,
                                      'Pros' : Pros,
                                      'Cons' : Cons,
                                      'User_Rating' : Rating,
                                      'Company':Company})
