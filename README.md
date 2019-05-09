# Lab2

学院：软件学院  班级：4班  学号：3017218151  姓名：代有为
日期：2019年4月
Sanford.Multimedia.Midi

Windows Form实现MIDI音乐文件的播放APP.

功能概述：能够正常播放MIDI音乐文件，对GUI界面中的控件大小、位置进行完善，使控件能够随APP界面大小自动       调整其自身大小。使界面底色变为淡蓝色，提升用户体验。
代码总量：添加70行代码。
工作时间：半天。
实验过程：Form1 Relize事件:Form_Resize
         Form1_Resize函数，控制控件大小随窗体改变
        
        public Form1()
        {
            InitializeComponent();
            this.TransparencyKey = Color.Red;
            this.BackColor = Color.LightBlue;
            int count = this.Controls.Count * 2 + 2;
            float[] factor = new float[count];
            int i = 0;
            factor[i++] = Size.Width;
            factor[i++] = Size.Height;
            foreach (Control ctrl in this.Controls)
            {
                factor[i++] = ctrl.Location.X / (float)Size.Width;
                factor[i++] = ctrl.Location.Y / (float)Size.Height;
                ctrl.Tag = ctrl.Size;
            }
            Tag = factor;
        }
         private void Form1_Resize(object sender, EventArgs e)
        {
            float[] scale = (float[])Tag;
            int i = 2;

            foreach (Control ctrl in this.Controls)
            {
                ctrl.Left = (int)(Size.Width * scale[i++]);
                ctrl.Top = (int)(Size.Height * scale[i++]);
                ctrl.Width = (int)(Size.Width / (float)scale[0] * ((Size)ctrl.Tag).Width);
                ctrl.Height = (int)(Size.Height / (float)scale[1] * ((Size)ctrl.Tag).Height);

                //每次使用的都是最初始的控件大小，保证准确无误。
            }
            
        }
实验结果：
     修改前：
     ![修改前](https://github.com/Dai-Youwei/lab2/blob/master/midi1.PNG )
     修改后：
     ![修改后](https://github.com/Dai-Youwei/lab2/blob/master/midi2.PNG)
