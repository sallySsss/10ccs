# 10ccs
 // Обробник події натискання кнопки "Розшифрувати"
 private void DecryptButton_Click(object sender, EventArgs e)
 {
     SymmetricAlgorithm alg = DefineAlg();
     ICryptoTransform cryptor = CreateDec(alg);

     using (FileStream fs = new FileStream(GetFileName(), FileMode.Open))
     {
         using (CryptoStream crStream = new CryptoStream(fs, cryptor, CryptoStreamMode.Read))
         {
             using (BinaryReader sr = new BinaryReader(crStream))
             {
                 FileInfo f = new FileInfo(GetFileName());
                 UnicodeEncoding enc = new UnicodeEncoding();
                 plaintextTextBox.Text = enc.GetString(sr.ReadBytes((int)f.Length));
             }
         }
     }
 }
