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

# Metadata
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
const url = "https://jsonplaceholder.typicode.com/todos";
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

# Loading
```
/app
  /about
    /page.tsx
    /Loading.tsx
```
# Error
```
/app
  /about
    /page.tsx
    /Loading.tsx
    /Error
```
# Params // Parameter
 ```
Route
/app
  /about
    /page.tsx
      /[id]
        /page.tsx
    /Loading.tsx
    /Error.tsx
/*--------------------------------------------------------------------------------------------*/
const Page = async ({ params }) =>{
/* {id} เป็น Destructuring คือการประกาศตัวแปรชื่อเดียวกับ Key เพื่อแกะข้อมูลออกมาจาก params*/
  const {id} = awit params.id;
  return
 <div>
    {id}
 </div>
};
export default Page
 ```
# Image
 ```
import Image form "next/image";

const url ="https://fastly.picsum.photos/id/0/5000/3333.jpg?hmac=_j6ghY5fCfSD6tvtcV74zXivkJSPIfR9B8w34XeQmvU";

const page = ()=>{
  return(
      <div>
          <Image
          src={url}
          width={xxx}
          height={xxx}
          alt="xxx"
          priority
           />
    <div>
)
}

 ```
# next.config.ts
เป็นการตั้งค่า file master เรื่อง potocall // ทุกครั้งที่ตั้งค่าต้อง restart server ทุกครั้ง
- ช่วยให้การจัดการภาพในเว็บไซต์มีประสิทธิภาพมากขึ้นโดยอัตโนมัติ
- ปรับขนาดภาพให้เหมาะสม ลดการเลื่อนเลย์เอาต์ และเพิ่มความเร็วในการโหลดหน้าเว็บ
 ```
import type { NextConfig } from "next";

const nextConfig: NextConfig = {
  /* config options here */
  images: {
    remotePatterns: [
      {
        protocol: "https",
        hostname: "fastly.picsum.photos", /* <<<  ลิงค์จากเว็บไซต์ */
        pathname: "/**", /* << ถ้าเราไม่ทราบ */
      },
    ],
  },
};

export default nextConfig;
 ```
# Server Actions
 ```
--------
Route
--------
/app
  /Input
    /Page.tsx
/components
  /Form.tsx
/utils
  /actions.ts


---------------------------
Page.tsx
---------------------------
import Form from "@/components/Form"
//rafce
const Page = () =>{
  return(
<div>
<Form />
</div>
)
}
export default Page

------------------------------
Form.tsx
------------------------------
'use client'
import { Cratedata } from "@/utils/actions";
const Form = () =>{
return <form action={Cratedata}>
        Form
        <input clssName = "border"
               name="title"
               placeholder = "xxxxx"
               defaultValue = "XXXXX"
        / >
        <input clssName = "border"
               name="location"
               placeholder = "xxxxx"
               defaultValue = "XXXXX"
        / >
        <button type="submit">Submit</button>
        </form>;
};

---------------------------
actions.ts
---------------------------
Server Actions
// จัดการข้อมูลจาก form -> formData.get('name')
// CRUD ข้อมูล -> mutate data (server)
// รีเฟรชข้อมูล -> revalidate cache
---------------------------
'use server'
import { revalidatePath } from "next/cache"
export const Cratedata = async(formData) =>{
   const rawData = Object.fromEntries(formData)
   console.log(rawData)
  --------------------------------------------------------------
  revalidatePath('/') //เป็นการ refresh ข้อมูลหน้าเดิม  *** สำคัญ ***
  redirect('/') //เมื่อทำงานเสร็จอยากให้เขาไปหน้าไหนต่อ
  ---------------------------------------------------------------
  return 'Input Success !!'
}

 ```

useActionState(), useFormStatus()
API
Middleware
TypeScript
