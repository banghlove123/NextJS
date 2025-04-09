https://ui.shadcn.com/docs/components/carousel
https://nextjs.org/docs/messages/css-global
https://tailwindcss.com/docs/installation/using-vite


# พื้นฐานที่จำเป็น
```
HTML 
CSS 
Javascript เบื้องต้น
Type Script
Function,Arrow function,Call back function
Object {}
Array []
Destruturing
.map()
```

พื้นฐานต้องควรรู้ NextJS 15
--
#Routing
คือ Layout ของโปรเจ็คที่ต้องการให้ Link หน้า Page
```
/app
  /about
    /page.tsx          # http://localhost:3000/about
  /info
    /page.tsx          # http://localhost:3000/info
          [id]         # [id] params folder
            /page.tsx  # http://localhost:3000/info/123456
  /_folder             # Private Folder (no public access)
  /(auth)              # Groups Folder
    /login
        /page.tsx      # http://localhost:3000/login
    /[...sign-in]         # params
        /page.tsx      # http://localhost:3000/sign-in
    /register
        /page.tsx      # http://localhost:3000/register
```

# Metadata </br>
คือตัวที่ช่วยเพิ่มประสิทธิภาพของ Share Engine</br>
```
import type { Metadata } from "next";
export const metadata: Metadata = {
  title: "Roitai", </br>
  description: "Camping in Thailand.",
  keywords: "Camping, Thailand, Roitai",
};
```
# Server Components
คือ componentที่ทำงานของฝั่ง Server เท่านั้น โดยโค้ดจะไม่ถูกส่งไปยัง Browser  

# Client Components
ถ้าจะใช้ต้องเพิ่มคำว่า 'use client'
- Client Components สามารถใช้ state, effects และ event listeners
- สามารถใช้ Browser APIs เช่น geolocation หรือ localStorage
```
'use client'
import { useState } from "react";
//rafce
const page = ()=>{
  cost[count,setCount] = useState(0)
return(
  <div>
    Page
  </div>
);
};
export default Page
```
# Fetch Data
```
const url = "...path API";
//rafce
/*การดึงข้อมูลจาก JSON มาแปลงในรูปแบบ DATA*/
const fetchTodo = async ()=>{
  const response = awit fetch(url);
  const data = awit res.json()
  return data;
};

const  Page = async ()=> {

  const data = await fetchTodo();
  console.log(data); /* ข้อมูลเป็น Arry */
  return
    <div>
    Page
    {
        /*เป็น method ทีเข้าไป Loop Arry  Syntax : array.map((currentValue, index, arr)=>)*/
        data.map((item,index)=>{
                return <div>
                    {item.title}
                      </div>
            })  
    }
    <div>
};
export default Page;



```

Loading, Error, Params, Image
Server Actions
useActionState(), useFormStatus()
API
Middleware
TypeScript
