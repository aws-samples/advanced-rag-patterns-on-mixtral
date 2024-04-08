# Advanced RAG Patterns with Mixtral on SageMaker Jumpstart

Example Jupyter Notebook of [Mixtral 8x7B Instruct](https://huggingface.co/mistralai/Mixtral-8x7B-Instruct-v0.1) and [BGE Large En](https://huggingface.co/BAAI/bge-large-en) to experiment Advanced Retrieval Augmented Generation (RAG) QnA systems on a SageMaker Notebook using [LangChain](https://www.langchain.com/).

See the accompanying blog post on the [AWS Machine Learning Blog](https://aws.amazon.com/blogs/machine-learning/advanced-rag-patterns-on-amazon-sagemaker/) for a detailed description.

## :books: Background

[Amazon SageMaker](https://aws.amazon.com/sagemaker/) is a fully managed service for data science and machine learning (ML) workflows.
You can use Amazon SageMaker to simplify the process of building, training, and deploying ML models.

The [SageMaker example notebooks](https://sagemaker-examples.readthedocs.io/en/latest/) are Jupyter notebooks that demonstrate the usage of Amazon SageMaker.

The [Sagemaker Example Community repository](https://github.com/aws/amazon-sagemaker-examples-community) are additional notebooks, beyond those critical for showcasing key SageMaker functionality, can be shared and explored by the commmunity.

## Prerequisites

### Sagemaker Prerequisites

In this section, you sign up for an AWS account and create an AWS Identity and Access Management (IAM) admin user.

If you're new to SageMaker, we recommend that you read [What is Amazon SageMaker?](https://docs.aws.amazon.com/sagemaker/latest/dg/whatis.html).

Follow the hyperlinks below to finish setting up the prerequisites for Sagemaker

-   [Create an AWS Account](https://docs.aws.amazon.com/sagemaker/latest/dg/gs-set-up.html#gs-account) - This walks you through setting up an AWS account
-   When you create an AWS account, you get a single sign-in identity that has complete access to all of the AWS services and resources in the account. This identity is called the AWS account root user.
-   Signing in to the AWS console using the email address and password that you used to create the account gives you complete access to all of the AWS resources in your account. We strongly recommend that you not use the root user for everyday tasks, even the administrative ones.
-   Instead, adhere to the Security best practices in [IAM](https://docs.aws.amazon.com/sagemaker/latest/dg/security-iam.html), and [Create an Administrative User and Group](https://docs.aws.amazon.com/sagemaker/latest/dg/gs-set-up.html#gs-account-user). Then securely lock away the root user credentials and use them to perform only a few account and service management tasks.
  

Once you are done with the above steps, you can move on to the one below

- The Mixtral 8x7b model requires an ml.g5.48xlarge instance. Amazon SageMaker JumpStart provides a simplified way to access and deploy over 100 different open source and third-party foundation models. In order to [launch an endpoint to host Mixtral 8x7B from SageMaker JumpStart](https://docs.aws.amazon.com/sagemaker/latest/dg/jumpstart-deploy.html), you may need to request a service quota increase to access an ml.g5.48xlarge instance for endpoint usage. You can easily [request service quota increases](https://docs.aws.amazon.com/servicequotas/latest/userguide/request-quota-increase.html) through the AWS console, CLI, or API to allow access to those additional resources.
  
## Architecture

![](docs/Architecture.drawio.png)

## Solution

In this repo we deploy a notebook, explain, and demonstrate the use of Mixtral 8x7B Instruct text generation combined with  [BGE Large En](https://huggingface.co/BAAI/bge-large-en) embedding model to efficiently construct a Retrieval Augmented Generation (RAG) QnA system on a [SageMaker](https://www.googleadservices.com/pagead/aclk?sa=L&ai=DChcSEwjC_smL6eSEAxUEaEcBHZKoCSwYABAAGgJxdQ&ase=2&gclid=CjwKCAiAi6uvBhADEiwAWiyRdm9fVXFJASMNG1LKo8hiUv7jEdUGhQ51tmCA-DngfHXsGDxLTBupFxoCvOcQAvD_BwE&ohost=www.google.com&cid=CAESVuD21B3o9zHMrlIQeG15m__r93DdZcVN4-3nXJ8u-dbMgnV5nBVFDPVOeevCZP5QgBP14_Qeor3zFwnOSibAEKrO6aqVYLSUyGSmJPwkoSC1y-dk0RNh&sig=AOD64_1g7baA79iO0oQhm2pU4_You-GQgQ&q&nis=4&adurl&ved=2ahUKEwjqhL-L6eSEAxUqD1kFHbRFAUEQ0Qx6BAgHEAE) Notebook using the Parent Document Retriever tool and Contextual Compression technique. This solution can be deployed with just a few clicks using [SageMaker JumpStart](https://aws.amazon.com/sagemaker/jumpstart/), a fully-managed platform that offers state-of-the-art foundation models for various use cases such as content writing, code generation, question answering, copywriting, summarization, classification, and information retrieval. It provides a collection of pre-trained models that can be deployed quickly and easily, accelerating the development and deployment of machine learning applications. One of the key components of SageMaker Jumpstart is the Model Hub, which offers a vast catalog of pre-trained models such as the Mixtral 8x7B for a variety of tasks.

The Jupyter notebook for this solution is in [Sagemaker-Advanced-RAG-langchain](https://github.com/aws-samples/advanced-rag-patterns-on-mixtral/blob/main/notebooks/sagemaker-advanced-rag-langchain.ipynb) 


## Parent Document Retriever Workflow

![](docs/cntxt.png)

## Contextual Compression Workflow

![](docs/pdr.png)

## :hammer_and_wrench: Setup

The quickest setup to run example notebooks includes:
- An [AWS account](http://docs.aws.amazon.com/sagemaker/latest/dg/gs-account.html)
- Proper [IAM User and Role](http://docs.aws.amazon.com/sagemaker/latest/dg/authentication-and-access-control.html) setup
- An [Amazon SageMaker Notebook Instance](http://docs.aws.amazon.com/sagemaker/latest/dg/gs-setup-working-env.html)

## Comparison of results
---------------

The following table compares results from different queries based on technique.

|

**Technique**

 |

           Regular Retriever Chain

 |

     Parent Document Retriever

 |

LLM Chain Extractor: Contextual Compression

 |

LLM Chain Filter: Contextual Compression

 |
|

**  Query 1**

How did AWS evolve?

 |

AWS (Amazon Web Services) evolved from an initially unprofitable investment to an $85B annual revenue run rate business with strong profitability, offering a wide range of services and features, and becoming a significant part of Amazon's portfolio. Despite facing skepticism and short-term headwinds, AWS continued to innovate, attract new customers, and migrate active customers, offering benefits such as agility, innovation, cost-efficiency, and security. AWS also expanded its long-term investments, including chip development, to provide new capabilities and change what's possible for its customers.

 |

AWS (Amazon Web Services) started with a feature-poor initial launch of the Elastic Compute Cloud (EC2) service in 2006, providing only one instance size, in one data center, in one region of the world, with Linux operating system instances only, and without many key features like monitoring, load balancing, auto-scaling, or persistent storage. However, AWS's success allowed them to quickly iterate and add the missing capabilities, eventually expanding to offer various flavors, sizes, and optimizations of compute, storage, and networking, as well as developing their own chips (Graviton) to push price and performance further. AWS's iterative innovation process required significant investments in financial and people resources over 20 years, often well in advance of when it would pay out, to meet customer needs and improve long-term customer experiences, loyalty, and returns for shareholders.

 |

AWS evolved by starting as a small project inside Amazon, requiring significant capital investment and facing skepticism from both inside and outside the company. However, AWS had a head start on potential competitors and believed in the value it could bring to customers and Amazon. AWS made a long-term commitment to continue investing, resulting in over 3,300 new features and services launched in 2022. AWS has transformed how customers manage their technology infrastructure and has become an $85B annual revenue run rate business with strong profitability. AWS has also continuously improved its offerings, such as enhancing EC2 with additional features and services after its initial launch.

 |

AWS (Amazon Web Services) evolved by initially launching feature-poor but iterating quickly based on customer feedback to add necessary capabilities. This approach allowed AWS to launch EC2 in 2006 with limited features and then continuously add new functionalities, such as additional instance sizes, data centers, regions, operating system options, monitoring tools, load balancing, auto-scaling, and persistent storage. Over time, AWS transformed from a feature-poor service to a multi-billion-dollar business by focusing on customer needs, agility, innovation, cost-efficiency, and security. AWS now has an $85B annual revenue run rate and offers over 3,300 new features and services each year, catering to a wide range of customers from start-ups to multinational companies and public sector organizations.

 |
|

Why is Amazon successful?

 |

Amazon is successful due to its continuous innovation and expansion into new areas such as technology infrastructure services, digital reading devices, voice-driven personal assistants, and new business models like the third-party marketplace. Its ability to scale operations quickly, as seen in the rapid expansion of its fulfillment and transportation networks, also contributes to its success. Additionally, Amazon's focus on optimization and efficiency gains in its processes has resulted in productivity improvements and cost reductions. The example of Amazon Business highlights the company's capability to leverage its e-commerce and logistics strengths in different sectors.

 |

Amazon is successful due to its ability to constantly innovate, adapt to changing market conditions, and meet customer needs in various market segments. This is evident in the success of Amazon Business, which has grown to drive roughly $35B in annualized gross sales by delivering selection, value, and convenience to business customers. Amazon's investments in ecommerce and logistics capabilities have also enabled the creation of services like Buy with Prime, which helps merchants with direct-to-consumer websites drive conversion from views to purchases.

 |

Based on the provided context, Amazon's success can be attributed to its strategic expansion from a book-selling platform to a global marketplace with a vibrant third-party seller ecosystem, early investment in AWS, innovation in introducing the Kindle and Alexa, and substantial growth in annual revenue from 2019 to 2022. This growth led to the expansion of the fulfillment center footprint, creation of a last-mile transportation network, and building a new sortation center network, which were optimized for productivity and cost reductions.

 |

Amazon is successful due to its innovative business models, continuous technological advancements, and strategic organizational changes. The company has consistently disrupted traditional industries by introducing new ideas, such as an ecommerce platform for various products and services, a third-party marketplace, cloud infrastructure services (AWS), the Kindle e-reader, and the Alexa voice-driven personal assistant. Additionally, Amazon has made structural changes to improve its efficiency, such as reorganizing its US fulfillment network to decrease costs and delivery times, further contributing to its success.

 |
|

Comparison

 |

- Based on the responses from the Regular Retriever Chain, we notice that although it provides long winded answers, it suffers from context overflow and fails to mention any significant details from the corpus in regards to responding to the query provided.

- The regular retrieval chain is not able to capture the nuances with depth or contextual insight, potentially missing critical aspects of the document.

 |

- The Parent Document Retriever delves deeper into the specifics of AWS's growth strategy, including the iterative process of adding new features based on customer feedback and the detailed journey from a feature-poor initial launch to a dominant market position, all while providing a context rich response.

- Responses cover a wide range of aspects, from technical innovations and market strategy to organizational efficiency and customer focus, providing a holistic view of the factors contributing to success along with examples. This can be attributed to PDR's targeted yet broad-ranging search capabilities.

 |

- The LLM Chain Extractor maintains a balance between covering key points comprehensively and avoiding unnecessary depth.

- Dynamically adjusts to the query's context, ensuring the output is directly relevant and comprehensive.

 |

Similar to the LLM Chain Extractor, the LLM Chain Filter ensures that while the key points are covered , the output is efficient for customers looking for concise and contextual answers.

 |

Upon comparing these different techniques, we can see that in contexts like detailing AWS's transition from a simple service to a complex, multi-billion-dollar entity, or explaining Amazon's strategic successes, the regular retriever chain lacks the precision the more sophisticated techniques offer, leading to less targeted information. Although quite a few differences are visible between the advanced techniques discussed, they are by far more informative than regular retriever chains.

For customers in industries such as healthcare, telecommunications, and financial services who are looking to implement RAG in their applications, the limitations of the regular retriever chain in providing precision, avoiding redundancy, and effectively compressing information make it less suited to fulfilling these needs compared to the more advanced parent document retriever and contextual compression techniques. These techniques are able to distill vast amounts of information into the concentrated, impactful insights that you need, while helping improve price-performance.

## Contributing

For any specific questions on how to contribute, please contact [armdiazg@amazon.com](https://www.linkedin.com/in/armando-diaz-47a498113/), [vijeasns@amazon.com](https://www.linkedin.com/in/niithiyn-vijeaswaran-451245213/), [bustils@amazon.com](https://www.linkedin.com/in/sebastian-bustillo/), [puniomp@amazon.com](https://www.linkedin.com/in/marcpunio/), [farsabir@amazon.com](https://www.linkedin.com/in/farooqsabir/), and [aboujid@amazon.com](https://www.linkedin.com/in/aj-dhimine-34a8b01ba/).

We welcome community contributions! Please see [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

## Security

See [CONTRIBUTING](CONTRIBUTING.md#security-issue-notifications) for more information.

## License

This library is licensed under the MIT-0 License. See the [LICENSE](LICENSE) file.
